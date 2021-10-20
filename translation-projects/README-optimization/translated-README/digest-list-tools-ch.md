# 摘要清单工具

## 描述

完整性度量架构 (IMA) 是Linux内核中的一个软件，用于测量执行execve()、mmap()、和open()系统调用访问的文件。测量结果可以发送至远程验证器或与参考值比较，以进行评估。

IMA摘要清单扩展程序储存在操作系统软件的内核内存参考值中，并且仅当这些值不包含测量的文件摘要时，才会在测量列表添加新条目。这种新型IMA度量清单应用不同的PCR，仅包含摘要清单和未知文件，可以在内核命令行中通过选项“ima_digest_list_pcr=#PCR”指定。 

此程序扩展的主要目的是克服测量OS文件时的一大挑战：由于二者并行执行，文件可以以不同的顺序进行访问，OS运行时的最终 PCR 值不可预测。

使用摘要清单扩展则不会出现这个问题，因为更新PCR时只会用到预加载的摘要清单的测量值。如果文件摘要可以在清单中找到，PCR不会进一步扩展。如果没有找到，PCR 就会扩展未知文件的摘要。

IMA摘要清单扩展还可用于评估时授予文件访问权限。有两种可能的用法：在清单中可以找到文件内容的摘要时，授予访问权限，由于不考虑元数据，因此这种方式安全性较低；在清单中可以找到元数据的摘要时，授予访问权限，这种方式更安全，因为受EVM保护的扩展属性和inode属性的当前值必须与创建（如，由供应商创建）摘要清单时设置的值匹配。

有关扩展程序的更多信息，请访问以下网址：

https://github.com/euleros/linux/wiki/IMA-Digest-Lists-Extension



## 软件架构

摘要清单工具提供了配置IMA摘要清单扩展程序所需的一组工具：

- gen_digest_lists:
  生成不同来源的摘要清单，例如RPM数据库、RPM包或文件夹；
  
- manage_digest_lists:
  管理摘要清单，将任意格式的摘要清单转换为内核支持的格式；
  
- upload_digest_lists:
  运行摘要清单解析器，上传内核无法识别的格式；
  
- verify_digest_lists:
  验证摘要清单的完整性；

- setup_ima_digest_lists:
  生成摘要清单，并可选择更新初始RAM磁盘，包括刚刚创建的摘要清单；
  
- setup_ima_digest_list_demo:
  运行带有预定义工作流程的脚本，创建摘要清单。

manage_digest_lists 和 gen_digest_lists 都采用模块化设计：都支持额外的解析器和生成器。第三方数据库应该放在$libdir/digestlist文件夹中。



### 生命周期

    gen_digest_lists:
                      +----------------------+
                      |  来源   (如： RPM DB) | (1) 提供来源
                      +----------------------+
                                 |
                                 |
    +------------+        +-------------+  (3) 生成摘要清单并签名
    |    生成器  1|   ...  |    生成器  N | ---------------------------------|
    +------------+        +-------------+                                  |
    +-----------------------------------+       +-------------+            |
    |     基准库    (I/O, xattr, crypto) | <---- |    签名密钥   |            |
    +-----------------------------------+       +-------------+            |
                                           (2) 提供签名密钥         |
                                                         +------+--------------+
                                                         | 签名  |    摘要清单   |
                                                         |      |    (fmt N)   |
                                                         +------+--------------+
    manage_digest_lists:                                                   |
                             (4) 解析摘要清单 (fmt N)                 |
    +----------+             +----------+                                  |
    |  解析器 1 |     ...     |  解析器 N | <--------------------------------|
    +----------+             +----------+                                  |
    +-----------------------------------+                                  |
    |        压缩清单API   (生成器)       | (5) 转换为压缩清单并签名             |
    +-----------------------------------+                                  |
    +-----------------------------------+       +-------------+            |
    |             基库      (I/O)        | <---- |  签名密钥    |            |
    +-----------------------------------+       +-------------+            |
                          |                                                |
                          |                                                |
                          |                                                |
    upload_digest_lists:  |                                                |
                          |      (6) 上传摘要清单                  +------------+
              +-------------+                                    |    解析器   |
              |    内核      | <--------------------------------- |   运行程序  |
              +-------------+                                    +------------+



### 摘要清单类别

我们已对摘要清单类别进行界定，限定在不同目的下摘要清单的使用。

- COMPACT_KEY:
  此类摘要清单包含用于验证其它摘要清单签名的公钥。
- COMPACT_PARSER:
  此类摘要清单包含解析器可执行文件的摘要及其共享库（包括支持新摘要清单格式的基库）。没有此类摘要，IMA将拒绝用户空间上传转换后的摘要清单。
- COMPACT_FILE:
  此类摘要清单包含一般性文件的摘要。
- COMPACT_METADATA:
  此类摘要清单包含文件元数据的摘要，其计算方式与EVM轻便式签名相同。

### 摘要清单编辑器

摘要清单编辑器用于为摘要清单类型提供附加属性。

- COMPACT_MOD_IMMUTABLE:
  在强制评估模式下，编辑器会限制文件的使用。摘要含此编辑器的文件能以只读模式打开。



### 摘要清单文件夹

默认情况下，所有摘要清单都存储在/etc/ima/digest_lists文件夹中。
文件格式如下：

<#position>-\<digest list type>_list-\<format>-\<filename>

例如，一个标准的摘要清单文件夹内容如下：

```
/etc/ima/digest_lists/0-metadata_list-rpm-libxslt-1.1.29-4.fc27-x86_64
/etc/ima/digest_lists/0-metadata_list-rpm-sqlite-libs-3.20.1-2.fc27-x86_64
/etc/ima/digest_lists/0-metadata_list-rpm-xkeyboard-config-2.22-1.fc27-noarch
```


## 安装

### 用例——可执行代码的测量与评估

此设置程序可用于评估二进制文件、共享库和带有摘要清单的脚本。

#### 测量的前提

- 通过执行以下命令检查RPM数据库中的摘要算法：

```
  rpm -q systemd --queryformat "%{RPMTAG_FILEDIGESTALGO}\n"
```

  可以在以下位置检索ID和摘要算法之间的关联：
  https://tools.ietf.org/html/rfc4880#section-9.4

- 添加到内核命令行：

```
  ima_hash=<hash algo>
```

#### 评估的前提

- 生成签名密钥和包含公钥的证书；
  可以使用内核源码中的certs/signing_key.pem
- 将证书转换为DER格式并将其复制到/etc/keys：

```
  openssl x509 -in certs/signing_key.pem -out /etc/keys/x509_evm.der \
               -outform der
```

- 向x509_evm.der添加公钥中的密钥IMA签名
- 从内核命令行中删除'root=<device>'，并将下行添加到/etc/dracut.conf：

```
  kernel_cmdline+="root=<device>"
```

- 将下行添加到/etc/dracut.conf，以包含验证摘要清单的公钥：

```
  install_items+="/etc/keys/x509_ima.der /etc/keys/x509_evm.der"
```


#### 启动程序配置

建议创建以下条目，并将下列字符串添加到内核命令行。

1) 度量

```
   ima_digest_list_pcr=11 ima_policy="tcb|initrd"
```

2) 评估

```
   ima_digest_list_pcr=11 ima_policy="tcb|initrd|appraise_tcb|appraise_initrd" \
   ima_appraise=digest ima_appraise=enforce-evm
```

#### IMA策略

以下策略组必须写入/etc/ima/ima-policy：

```
measure func=MMAP_CHECK mask=MAY_EXEC
measure func=BPRM_CHECK mask=MAY_EXEC
measure func=MODULE_CHECK
measure func=FIRMWARE_CHECK
measure func=POLICY_CHECK
appraise func=MODULE_CHECK appraise_type=imasig
appraise func=FIRMWARE_CHECK appraise_type=imasig
appraise func=KEXEC_KERNEL_CHECK appraise_type=imasig
appraise func=POLICY_CHECK appraise_type=imasig
appraise func=BPRM_CHECK appraise_type=imasig
appraise func=MMAP_CHECK
```

MAP_CHECK钩子不应用IMA签名，因为某些进程（如firewalld）在tmpfs中映射为可执行文件。


#### 设置

在带有RPM包管理器的系统中，可以使用以下命令生成摘要清单：

```
# gen_digest_lists -t metadata -f rpm+db -i l: -o add -p -1 -m immutable \
   -i f:compact -i F:/lib/firmware -i F:/lib/modules -d /etc/ima/digest_lists \
   -i i: -i x: -i e:
```

上述命令只选定有执行位组的打包文件及/lib/firmware和/lib/modules中的文件，将IMA和EVM摘要添加到RPM数据库中所有文件包的摘要清单里。

如果内核中没有执行策略的硬编码，则需要为systemd创建一个完整的摘要清单，因为在systemd加载自定义策略之前，配置文件仍要接受测量和评估：

```
# gen_digest_lists -t metadata -f rpm+db -i l: -o add -p -1 -m immutable \
   -i f:compact -i F:/lib/firmware -i F:/lib/modules -d /etc/ima/digest_lists \
   -i i: -i x: -i p:systemd
```

使用自定义内核，还需要额外执行：

```
# gen_digest_lists -t metadata -f compact -i l: -o add -p -1 -m immutable \
   -i I:/lib/modules/`uname -r` -d /etc/ima/digest_lists -i i: -i x:
```

软件包管理器无法识别的其它文件也可以添加到摘要清单中：

```
# gen_digest_lists -t metadata -f unknown -i l: -o add -p -1 -m immutable \
   -i D:/etc/ima/digest_lists -i I:<desired directory> -d /etc/ima/digest_lists \
   -i i: -i x: -i e:
```

摘要清单创建后，必须用evmctl签署：

```
# evmctl sign -o -a sha256 --imahash --key <private key> -r \
   /etc/ima/digest_lists
```

重新生成初始RAM磁盘，并包含自定义 IMA 策略：

```
# dracut -f -exattr -I /etc/ima/ima-policy
```

要执行上述命令，包括初始RAM磁盘中的扩展属性，必须应用以下网站提供的补丁：

https://github.com/euleros/cpio/tree/xattr-v1  
https://github.com/euleros/dracut/tree/digest-lists


摘要清单将通过新的dracut模块“digestlist”（该软件的一部分），自动包含在初始RAM磁盘中。其配置文件在/etc/dracut.conf.d中。


#### 启动过程

在启动过程中尽量提前加载摘要清单，以便在访问文件之前找到摘要。内核会读取并解析 /etc/ima/digest_lists文件夹中的摘要清单。


#### 软件升级

如果系统上安装了新的RPM，则必须使用上述命令创建新的摘要清单。在重新生成初始RAM磁盘前，不会在启动时自动加载新的摘要清单。将生成一个systemd加载新的摘要清单，无需重新生成初始RAM磁盘。



### 用例——不变与可变文件（带HMAC密钥）

下述步骤仅代表某一配置示例。应包含在摘要清单中的文件列表和类型（不变或可变）取决于用户需求。设置过程分为两步。首先，系统启动救援模式，方便在安全环境下计算可变文件的摘要（此时文件不受程序访问）。

在第一步中，管理员运行setup_ima_digest_lists_demo脚本，为系统创建摘要清单。如果提前知道要测量或评估的所有文件的内容，则可以由软件商完成这一步。否则，管理员需通过签署摘要清单对系统将访问的文件的初始值负责。在此阶段，HMAC密钥尚不可用。密钥在摘要清单生成时立即产生并封存。

第二步，管理员在配置最后一步运行系统，解封HMAC密钥，但此时仍然选择救援模式。在这一步，管理员再次运行setup_ima_digest_lists_demo脚本，为每个用摘要清单验证的文件添加HMAC密钥。

#### 测量前提：

- 在/etc/fstab中添加“iversion”挂载选项（如果文件系统支持）
- 通过执行以下命令检查RPM数据库中的摘要算法：

```
  rpm -q systemd --queryformat "%{RPMTAG_FILEDIGESTALGO}\n"
```

  可以在以下位置检索ID和摘要算法之间的关联：
  https://tools.ietf.org/html/rfc4880#section-9.4

- add to the kernel command line:

```
  ima_hash=<hash algo>
```

#### 评估前提：

- 生成签名密钥和包含公钥的证书；
  可以使用内核源码中的certs/signing_key.pem
- 将证书转换为DER格式并将其复制到/etc/keys：

```
  openssl x509 -in certs/signing_key.pem -out /etc/keys/x509_ima.der \
               -outform der
```

- 生成EVM密钥；按下述说明操作：
  https://sourceforge.net/p/linux-ima/wiki/Home/, “创建可信和EVM加密密钥”部分
- 从内核命令行中删除'root=<device>'，并将下行添加到/etc/dracut.conf：

```
  kernel_cmdline+="root=<device>"
```

- 从GIT存储库中复制以下dracut模块：
  https://github.com/dracutdevs/dracut 到/usr/lib/dracut/modules.d:

```
  96securityfs 97masterkey 98integrity
```

- 添加下行到/etc/dracut.conf中，将dracut模块加进RAM磁盘：

```
  add_dracutmodules+=" securityfs masterkey integrity"
```

- 在/etc/dracut.conf中添加以下几行，将验证摘要清单的公钥和EVM密钥加进来：

```
  install_items+="/etc/keys/x509_ima.der"
  install_items+="/etc/keys/kmk-trusted.blob /etc/keys/evm-trusted.blob"
```

  （在最后一行，如果使用用户密钥作为主密钥，则用kmk-user替换kmk-trusted）

- 在/etc/dracut.conf中添加下行，在初始RAM磁盘中包含SELinux标签：

```
  install_items+="/etc/selinux/targeted/contexts/files/file_contexts"
  install_items+=/etc/selinux/targeted/contexts/files/file_contexts.subs_dist"
```


#### 启动程序配置

建议创建以下条目并将下列字符串添加到内核命令行：

1) 设置

```
   systemd.unit=setup-ima-digest-lists.service
```

2) 测量

```
   ima_digest_list_pcr=11 ima_policy="tcb|initrd"
```

3) 评估设置

```
   ima_digest_list_pcr=11 ima_policy="tcb|initrd|appraise_tcb|appraise_initrd| \
   appraise_tmpfs" ima_appraise=digest ima_appraise=enforce-evm evm=random
   systemd.unit=setup-ima-digest-lists.service
```

4) 评估

```
   ima_digest_list_pcr=11 ima_policy="tcb|initrd|appraise_tcb|appraise_initrd| \
   appraise_tmpfs" ima_appraise=digest ima_appraise=enforce-evm evm=random
```

5) 评估许可

```
   ima_digest_list_pcr=11 ima_policy="tcb|initrd|appraise_tcb|appraise_initrd| \
   appraise_tmpfs" ima_appraise=digest ima_appraise=log-evm evm=random
```


#### 设置-第一阶段

##### 使用RPM包管理器

摘要清单工具包含一个名为setup_ima_digest_lists_demo的脚本，简化摘要清单的创建。它将创建以下摘要清单：

- 来自文件包管理器的摘要清单
- 初始RAM磁盘中未知文件的摘要清单（部分由 dracut 生成）
- IMA策略摘要清单
- 根文件系统中未知文件的摘要清单，以便启用评估（注意：元数据摘要将从扩展属性的当前值创建；在生成和签署摘要清单之前，管理员必须进行检查）

1) 执行指令：

```
# setup_ima_digest_lists_demo initial [signing key] [X.509 certificate]
```

此为交互式过程，要求用户确认或编辑需要包含在摘要清单中的文件。

2) 重新启动

重启系统，在启动过程中加载新的摘要清单。

##### 不使用RPM包管理器

创建摘要清单的另一种方法是不使用包管理器，直接从文件系统中获取文件摘要。编辑setup_ima_digest_lists_demo并注释以“setup_ima_digest_lists distro”开头即可。


#### 设置-第二阶段

在设置的第一阶段之后，/etc/ima/digest_lists会包含启动系统所需的所有摘要清单，并启用并执行评估。剩下的步骤是为摘要清单中的每个文件添加一个HMAC密钥。

1) 执行指令：

```
# setup_ima_digest_lists_demo final
```

### 软件更新

#### Generation

可以使用gen_digest_lists工具生成摘要认证清单。可以执行以下命令：

```
$ man gen_digest_lists
```

### 完整性验证

加载摘要清单后，测量清单将如下所示：

```
11 <digest> ima-ng <digest> boot_aggregate
11 <digest> ima-ng <digest> /etc/keys/x509_ima.der
11 <digest> ima-ng <digest> [...]/0-parser_list-compact-manage_digest_lists
11 <digest> ima-ng <digest> [...]/0-key_list-signing_key.der
11 <digest> ima-ng <digest> [...]/1-parser_list-compact-libparser-ima.so
11 <digest> ima-ng <digest> [...]/2-parser_list-compact-libparser-rpm.so
11 <digest> ima-ng <digest> [...]/0-file_list-rpm-libxslt-1.1.29-4.fc27-x86_64
...
<measurement entries for modified mutable files>
```

证明服务器可以用verify_digest_lists工具验证摘要清单的完整性。例如，它可以执行：

```
$ verify_digest_lists
```


## 作者

Roberto Sassu, <roberto.sassu at huawei.com>.



## 版权

版权所有(C)2018-2020 Huawei Technologies Duesseldorf GmbH

在GNU公共许可证(2.0GPLv2)条款范围内免费试用本软件