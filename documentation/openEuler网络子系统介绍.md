# openEuler网络子系统相关介绍

参阅，推荐进一步阅读。

> [openEuler网络子系统: 介绍openEuler网络子系统架构 (gitee.com)](https://gitee.com/MrRlu/openeuler_network_subsystem#结语)
>
> [Linux内核网络（一）——初探内核网络 ](https://zhuanlan.zhihu.com/p/363718587)
>
> [openEuler-whitepaper-2109.pdf](https://www.openeuler.org/whitepaper/openEuler-whitepaper-2109.pdf)
>
> [使用XDP(eXpress Data Path)防御DDoS攻击](https://blog.csdn.net/dog250/article/details/77993218)

实现计算机之间的互联通信极其重要，计算机网络从一开始的目的就是实现不同计算机之间信息的传输和共享。操作系统作为底层软件，承担着通信模块中重要的角色。

> openEuler网络子系统负责网络IO，通过与网络设备（路由器、交换机等）的数据交互，实现端到端的数据交互过程。

本文通过梳理计算机网络的模型，简单介绍了openEuler中的网络子系统，并介绍了openEuler内核在网络通信方面的创新技术点，使得读者可以对openEuler的网络子系统有一定的了解。

## 网络模型

OSI七层参考模型是ISO制定的用于计算机或通信系统间互联的标准体系。其中规定了一系列抽象的术语概念和具体的协议。但在现实当中，TCP/IP 五层模型通过快速占领了市场（第一代表一切）获得了实际的话语权。TCP/IP 凭借只包含应用层，传输层，网络层，链路层，物理层五个模型，大大减少了硬件厂商的工作量。如果将OSI对应过去的话，在TCP/IP中，OSI的表示层、和会话层，一并交给应用层来处理。

计算机网络解决的是端到端的通信，在数据面上来看，几乎每一层都是直接与另一端的同一层进行交流，无需顾忌底层的细节。下面简单介绍以下五层模型的主要功能。

- 物理层：主要负责物理上的数据包传输，如WiFi、以太网等协议；
- 数据链路层：主要负责处理端点间的数据传输；
- 网络层：负责数据包转发和主机编码；
- 传输层：完成结点间的数据发送；
- 应用层：各类应用层协议，如常用的HTTP、FTP；

对于操作系统而言，一般不涉及物理层和应用层，所以大部分情况只需要聚焦于

1. 链路层数据协议解析：接收到数据包时，向上传递给网路层，由目的地决定后续操作；
2. 网络层协议解析：分析目的地，如为本机则上传，否则则交还给数据链路层传输；
3. 传输层发送：发送数据包时，给定数据包格式，依次下发。

## Linux子系统

Linux 作为通用操作系统，需要可以兼容大部分硬件。因此在实际涉及时，必须通过逻辑抽象，各个参数支持设定，以此淡化物理设备的差异。举一个linux网络设备中最关键的一个结构体为例`net_device`。

```c
struct net_device {
	char			name[IFNAMSIZ];
	struct netdev_name_node	*name_node;
	struct dev_ifalias	__rcu *ifalias;
	/*
	 *	I/O specific fields
	 *	FIXME: Merge these and struct ifmap into one
	 */
	unsigned long		mem_end;
	unsigned long		mem_start;
	unsigned long		base_addr;
	int			irq;

	/*
	 *	Some hardware also needs these fields (state,dev_list,
	 *	napi_list,unreg_list,close_list) but they are not
	 *	part of the usual set specified in Space.c.
	 */

	unsigned long		state;

	struct list_head	dev_list;
	struct list_head	napi_list;
	struct list_head	unreg_list;
	struct list_head	close_list;
	struct list_head	ptype_all;
	struct list_head	ptype_specific;

	struct {
		struct list_head upper;
		struct list_head lower;
	} adj_list;

	netdev_features_t	features;
	netdev_features_t	hw_features;
	netdev_features_t	wanted_features;
	netdev_features_t	vlan_features;
	netdev_features_t	hw_enc_features;
	netdev_features_t	mpls_features;
	netdev_features_t	gso_partial_features;

	int			ifindex;
	int			group;
	……
```

[具体代码可以自行查看](https://github.com/openeuler-mirror/native-turbo-kernel/blob/62f8a4e02acf2a3367942f70f127def4138dd213/include/linux/netdevice.h#:~:text=struct%20net_device%20%7B,int%09%09%09group%3B)，网络设备驱动作为数据链路层的主要实现，主要完成两个任务

- 接收数据包并传递给网络层
- 传出数据包给其他端

该结构体作为对网络设备的抽象，包含了网络设备驱动相关的所有信息，但即使如此，在实际应用当中，也往往还需要额外定义信息。此时只需要自定义一个结构体，将`net_device`结构体作为成员包含进去。使用时需要先通过register_netdev() 函数注册设备，并自行定义数据结构等进行实际操作。

这里我们可以看到，Linux 协议栈实现从链路层通用处理到 IP 层路由，都是通过支持一些函数调用实现的。

> 记住，OSI 模型也好，TCP/IP 模型也罢，所谓的分层仅仅是逻辑视图上的分层，好在让人们便于理解以及便于界定软件设计的边界和分工。

## XDP

在《OpenEuler21.09白皮书中》提到了一个内核创新点，那就是支持XDP。

> XDP：基于 ebpf 的 一种高性能、用户可编程的网络数据包传输路径， 在网络报文还未进入网络协议栈之前就对数据进行处理，提升网络性能。可用于 DDOS 防御、防火墙、 网络 QOS 等场景。
>
>  XDP优势：可编程、内核协同工作 **可编程**：在网络硬件智能化趋势下，可编程可以适用多种场景。 **内核协同**：XDP并不是完全bypass kernel，所以在必要的时候可以与内核协同工作，利于网络统一管理、部署。

XDP通过 定义了一个受限的执行环境（a limited execution environment），运行在一个 eBPF 指令虚拟机中。在网卡收到包后最早能处理包的位置，做一些自定义数据包处理（包括重定向）。

例如，在服务器处理DDOS的时候，通过XDP，可以直接在内核里直接处理黑名单内的IP地址，大大提高了CPU的利用率。

