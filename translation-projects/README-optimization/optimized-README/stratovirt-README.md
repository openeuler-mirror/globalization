# StratoVirt
StratoVirt is an enterprise-grade virtualization platform for cloud data centers
in the computing industry. It implements a set of architecture that supports
three scenarios: virtual machines, containers, and serverless computing.  

StratoVirt has its competitive advantages in light weight, low memory overload, software
and hardware synergy, and Rust language-level security.  

StratoVirt reserves interfaces and designs for importing more features. It is evolving to standard virtualization.  

## How to Start

### Preparations
Before building StratoVirt, make sure that Rust language and Cargo have already
been installed. If not, read the installation guidance via the following link:  

https://www.rust-lang.org/tools/install  

You will get a smaller memory overhead if you prepare the musl toolchain for Rust.

### Build StratoVirt
To build StratoVirt, clone the project and build it first:  
```sh
$ git clone https://gitee.com/openeuler/stratovirt.git
$ cd stratovirt
$ cargo build --release
```
Now you will find StratoVirt binary in `target/release/stratovirt`.

### Run a VM with StratoVirt
To run StratoVirt quickly, you need:  
* A Linux kernel image of PE or bzImage (only x86_64) format
* A raw rootfs image of an EXT4 filesystem

You can obtain the kernel and rootfs images from the following link:  

https://repo.openeuler.org/openEuler-21.03/stratovirt_img/

For standard_vm, a firmware file of EDK2 which follows UEFI is required.  

```shell
# If the socket of qmp exists, remove it first.

# Start microvm
$ ./target/release/stratovirt \
    -machine microvm \
    -kernel /path/to/kernel \
    -append "console=ttyS0 root=/dev/vda reboot=k panic=1" \
    -drive file=/path/to/rootfs,id=rootfs,readonly=off \
    -device virtio-blk-device,drive=rootfs \
    -qmp unix:/path/to/socket,server,nowait \
    -serial stdio

# Start standard_vm
$ ./target/release/stratovirt \
    -machine standard_vm \
    -kernel /path/to/kernel \
    -append "console=ttys0 root=/dev/vda reboot=k panic=1" \
    -drive file=/path/to/firmware,if=pflash,unit=0,readonly=true \
    -device pcie-root-port,port=0x0,addr=0x1.0x0,bus=pcie.0,id=pcie.1 \
    -drive file=/path/to/rootfs,id=rootfs,readonly=off \
    -device virtio-blk-pci,drive=rootfs,bus=pcie.1,addr=0x0.0x0 \
    -qmp unix:/path/to/socket,server,nowait \
    -serial stdio
```

The detailed guidance for making rootfs, compiling the kernel, and building StratoVirt
can be found in [StratoVirt QuickStart](./docs/quickstart.md).  

StratoVirt supports many other more features, which can be found in [Configuration Guidebook](docs/config_guidebook.md).

## Design

To get more details about StratoVirt's core architecture design, refer to
[StratoVirt design](./docs/design.md).

## How to Contribute
We welcome new contributors! And we are happy to provide guidance and help for
new contributors. StratoVirt follows Rust formatting conventions, which can be
found at:  

https://github.com/rust-dev-tools/fmt-rfcs/tree/master/guide  
https://github.com/rust-lang/rust-clippy

You can get more information about StratoVirt at:  

https://gitee.com/openeuler/stratovirt/wikis  

If you find a bug or have some ideas, please send an email to the [virt mailing list](https://mailweb.openeuler.org/postorius/lists/virt.openeuler.org/) or submit an [issue](https://gitee.com/openeuler/stratovirt/issues).

## Licensing
StratoVirt is licensed under the Mulan PSL v2.
