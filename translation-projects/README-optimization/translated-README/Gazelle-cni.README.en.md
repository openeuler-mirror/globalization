# Gazelle-cni

#### Motivation

Gazelle is a user-mode protocol stack that has been commercialized within Huawei. It supports TCP/UDP protocol stack. Compared with similar software, Gazelle has many advantages in performance and applicability, including concurrency linearity, low latency, ease of use, etc. .

The effect drawing of performance reference acceleration Nginx is as follows:

![img](https://gitee.com/openeuler/gazelle-cni/raw/master/Nginx-2.png)

 Linearity is close to 1

![img](https://gitee.com/openeuler/gazelle-cni/raw/master/nginx-1.png)

Delays in transmission are small

Ease of use : no need to modify the code , no need to recompile , and only install acceleration Library.

The Gazelle-CNI  project is to open source of Huawei’s internal Gazelle commercial project and apply it to cloud-native scenarios. This project will be one of the important technologies to accelerate cloud-native ServiceMesh.

ServiceMesh of cloud-native scenarios has become a standard component in various cloud scenarios, and among them is the de facto standard implemented by istio. Envoy is the data plane component of istio, so the goal of this project is to accelerate the Envoy component.

#### Objective

Performance: Improve the performance of the service grid data plane, achieve a 30% reduction in the service access latency in the cluster, and a 30% increase in the service access throughput in the cluster.

Ease of use: open source istio is plug and play, with no code modifications and no rebuild required. 

#### Introduction

As the data plane component of istio, Envoy takes over all external data flows in the grid and achieves LB, statistics and other functions.  The data flow figure is as follows :

![img](https://gitee.com/openeuler/gazelle-cni/raw/master/envoy-1.png)

Among them, we can see that the entire data flow path is lengthy, and there is a bottleneck to the performance of the service grid. So we accelerate its entire data path, the acceleration plan is as follows:

![img](https://gitee.com/openeuler/gazelle-cni/raw/master/envoy-2.png)

The acceleration includes:

1. Gazelle CNI: Optimization based on Gazelle，the Huawei's internal commercial project.
2. Socket-map: Use eBPF's sockmap technology to realize the communication acceleration between sockets
3. XDP Bridge: Use XDP technology to implement the Bridge function and use it as the Bridge that kubelet pulls up by default.

#### Roadmap Planning (tentative)

1. Gazelle project open source:  Open source code before 2021.6.30.
2. Gazelle-CNI technology demo demonstration: The demo demonstration will be completed before 2021.3.30. Envoy can simultaneously apply the Gazelle protocol stack and the kernel protocol stack to complete single-node acceleration.
3. Gazelle-CNI technology development: Complete the CNI adaptation of the Gazelle project and AF_XDP adaptation before 2021.5.30.
4. Socket-map technology: Technology development will be completed before 2021.6.30.
5. XDP bridge technology: Technology development will be completed before 2021.7.30.

#### Join Us 

At present, Gazelle technology is mature, but other technologies, such as Gazelle-CNI, are currently in the design and prototype verification stage. If you are interested in our community, welcome to join us.

#### Contact Us

[high-performance-network@openeuler.org](mailto:high-performance-network@openeuler.org) [dev@openeuler.org](mailto:dev@openeuler.org)

