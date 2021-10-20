# Anbox

此代码仓是从https://github.com/anbox/anbox链接中克隆而成的，并将在欧拉开源社区安卓中间件下进行维护。我们致力于在本地Arm PC上运行Anbox。

Anbox采用基于容器的方式，在 Ubuntu 等常规 GNU/Linux操作系统上启用完整的安卓系统。换言之：Anbox可以让您在Linux操作系统中运行安卓系统，并且不像虚拟化那样缓慢。

## 产品概述

Anbox使用Linux namespaces技术在容器中运行完整的安卓系统，如user、pid、uts、net、mount、ipc，并在任何基于 GNU/Linux 操作系统上提供安卓应用程序。

容器内的安卓端无法直接访问任何硬件。所有硬件都是通过主机上的 anbox daemon程序进行访问。我们正在重新利用安卓端在基于 QEMU 的模拟器中实现的 OpenGL ES 加速渲染。容器内的安卓系统使用不同的管道与主机系统进行通信，并通过这些管道发送所有硬件访问命令。

您可以查看以下文件了解更多

 * [Android Hardware OpenGL ES 仿真设计概述](https://android.googlesource.com/platform/external/qemu/+/emu-master-dev/android/android-emugl/DESIGN)
 * [Android QEMU 高速管道](https://android.googlesource.com/platform/external/qemu/+/emu-master-dev/android/docs/ANDROID-QEMU-PIPE.TXT)
 * [The Android "qemud" 复用守护](https://android.googlesource.com/platform/external/qemu/+/emu-master-dev/android/docs/ANDROID-QEMUD.TXT)
 * [Android qemud 服务](https://android.googlesource.com/platform/external/qemu/+/emu-master-dev/android/docs/ANDROID-QEMUD-SERVICES.TXT)

Anbox 目前适用于电脑桌面，但也可用于移动操作系统，如 Ubuntu Touch、Sailfish OS 或 Lune OS。然而，由于安卓应用程序的映射目前是特定于桌面的，因此也需要对支持的堆叠窗口用户界面进行补充操作。

安卓运行时环境附带基于 [安卓开源项目](https://source.android.com/) 的最小定制安卓系统映像。

使用的图片目前基于Android 7.1.1版本。

## 支持的Linux发行版本

目前我们正式提供以下Linux发行版本：

 * Ubuntu 16.04 (xenial)
 * Ubuntu 18.04 (bionic)
 * UOS

其他发行版只要提供必需的内核模块就能正常工作（请参阅内核参数）。

 * [发行说明](docs/release-notes/anbox-release-notes.md)


## 从源代码构建

### 要求

建议在ARM64架构上运行。

构建Anbox运行时本身无需多言。我们使用Cmake编译工具作为构建系统。您的主机系统上需要以下构建依赖项：

 * libdbus
 * google-mock
 * google-test
 * libboost
 * libboost-filesystem
 * libboost-log
 * libboost-iostreams
 * libboost-program-options
 * libboost-system
 * libboost-test
 * libboost-thread
 * libcap
 * libsystemd
 * mesa (libegl1, libgles2)
 * libsdl2
 * libprotobuf
 * protobuf-compiler
 * lxc (>= 3.0)
 * libasound

在 Ubuntu 系统上，您可以使用以下命令安装所有构建依赖项：

```
$ sudo apt install build-essential cmake cmake-data debhelper dbus google-mock \
    libboost-dev libboost-filesystem-dev libboost-log-dev libboost-iostreams-dev \
    libboost-program-options-dev libboost-system-dev libboost-test-dev \
    libboost-thread-dev libcap-dev libsystemd-dev libegl1-mesa-dev \
    libgles2-mesa-dev libglm-dev libgtest-dev liblxc1 \
    libproperties-cpp-dev libprotobuf-dev libsdl2-dev libsdl2-image-dev lxc-dev \
    pkg-config protobuf-compiler libasound2-dev
```
建议您使用Ubuntu 18.04（仿生）和 **GCC 7.x**作为构建环境。

在 UOS 系统上，您可以使用以下命令安装所有构建依赖项：

```
$ sudo apt install gcc libncurses-dev bison flex libssl-dev cmake dkms build-essential \
    cmake-data debhelper dbus google-mock libboost-dev libboost-filesystem-dev libboost-log-dev \
    libboost-iostreams-dev libboost-program-options-dev libboost-thread-dev libcap-dev \
    libsystemd-dev libegl1-mesa-dev libgles2-mesa-dev libglm-dev libgtest-dev liblxc1 \
    libproperties-cpp-dev libprotobuf-dev libsdl2-dev libsdl2-image-dev lxc-dev libdw-dev \
    libbfd-dev libdwarf-dev pkg-config protobuf-compiler libboost-test-dev
```

### 构建

```
$ mkdir -p /home/compile/
$ cd /home/compile/
$ git clone https://gitee.com/openeuler/anbox
```

 * [应用SDL补丁](docs/apply_SDL_patch.md)
 * [安装binder & ashmem 模块](docs/kernel_module.md)

之后，您可以使用以下命令构建 Anbox：

```
$ cd /home/compile/anbox
$ mkdir build
$ cd build
$ cmake .. -DCMAKE_CXX_FLAGS="-DENABLE_TOUCH_INPUT -Wno-error=implicit-fallthrough \
    -Wno-error=missing-field-initializers" -DCMAKE_BUILD_TYPE=Release -DWerror=OFF
$ make -j8

```

如果您要选择版本，请执行以下操作：

```
$ git clone https://gitee.com/openeuler/anbox -b anbox-v1.0-rc3
```

anbox-v1.0-rc3 版本会在以后更新，请确保它与 AOSP 的版本匹配（请参阅 build-android.md。

示例

```
$ sudo make install
```

在您的系统上安装正确的位数。

## 运行Anbox

步骤1：启动容器管理器，以ROOT用户运行命令，你必须有一个android.img。

```
$ bash /usr/local/bin/anbox-bridge.sh start
$ anbox container-manager --android-image=/<your path>/android.img \
         --data-path=/<your path>/anbox-data --privileged --daemon &

```

步骤2：启动会话管理器，以非ROOT用户运行命令，并运行从桌面用户界面打开的shell终端。

```
$ export EGL_PLATFORM=x11
$ export EGL_LOG_LEVEL=fatal
$ anbox session-manager  --gles-driver=host &

```

等待30s，在应用栏中的“其他应用”中打开安卓APP。

## 说明

您将在项目源的 *docs* 子目录中找到 Anbox 的其他文档。

其他说明可查看：

 * [运行时设置](docs/runtime-setup.md)

## 漏洞报告

如果您发现 Anbox出现问题，请[提交错误](https://gitee.com/openeuler/anbox/issues)。

## 保持联系

寻找维护者：

https://gitee.com/openeuler/community/tree/master/sig/sig-android-middleware

## 版权和许可

Anbox 重复使用了来自其他项目（如 Android QEMU 模拟器）的代码。这些项目位于

external/ 子目录中，其中包含许可条款。

Anbox 源本身，如果在相关源文件中没有不同说明，则根据 GPLv3 许可条款获得许可。

