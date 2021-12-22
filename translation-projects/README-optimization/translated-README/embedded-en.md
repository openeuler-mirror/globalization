# embedded

#### 1 Introduction

Support the openEuler version of embedded devices, currently supports two CPU architectures [aarch64|x86_64].

#### 2 Compilation Instructions

build.sh is the compilation entry, used as follows:

```Usage: 
Usage: 

./build.sh -a [aarch64|x86_64] -r [repo] -d [work dir] -p [live|virtual|disk|docker] -t [rpm|image|all]
```

The function description of each parameter is as follows:

1)\- r, specify the repo file in the configuration file format of dnf/yum, please refer to [document1](https://docs.openeuler.org/zh/docs/20.03_LTS/docs/Administration/%E4%BD%BF%E7%94%A8DNF%E7%AE%A1%E7%90%86%E8%BD%AF%E4%BB%B6%E5%8C%85.html "使用DNF管理软件包").

2) -d, specify the working directory used in the compilation process, where all intermediate files and results are stored. Since the compilation process requires large disk space, the directory should be located in a disk with **≥20G** free space.

3) -p, specify the type of image to be compiled. Currently, docker image is stably supported.

4) -t, specify the compilation type. rpm refers to the rpm repository compiled according to the source code and patch; image refers to the specified image compiled according to the given repo; all will execute the compilation process specified by rpm and image in order.

5) a, no need to specify. Parameters supporting cross-compilation are reserved.

The structure of the working directory during normal compilation (- specified by the d parameter) is as follows:

```
allsrcpath.list         // List of packages to be compiled according to package_conf.xml
image/                  // Storage location of the image and its description file
kiwiconfig/
logs_1.tar.gz           // Compilation log of each package in round 1/2
logs_2.tar.gz           // Compilation log of each package in round 2/2
openeuler.repo
rpms/                   // The directory where the rpm package of each package is compiled, which can be referenced as a repo source
src/                    // Download and patch the source code files of each software package according to the configuration file
```

**Attention: if the compiled session (login terminal) is prone to disconnection, please use something like ```nohup sh build.sh -r ... > log.txt 2>&1 &```to execute the compilation**, avoiding compilation interruption caused by disconnection.

#### 3 Configuration File Description

The configuration files are located in the config directory: 

```
kiwiconf/
openeuler.repo
package_conf.xml
```

1)  ```kiwiconf/```, storing the configuration files required by the kiwicompat command. Generally, no changes are required.

The format of the config.xml refers to [document 2](https://documentation.suse.com/kiwi/9/single-html/kiwi/index.html#image-description-elements "image-description-elements")，[document 3](https://documentation.suse.com/kiwi/9/html/kiwi/image-description.html "image-description")。

Kiwi calls images.sh after creating the system directory. This script can be used to cut unnecessary files in the root directory or make some system settings. See [document 4](https://documentation.suse.com/kiwi/9/single-html/kiwi/index.html#script-template-for-config-sh-images-sh "script-template-for-config-sh-images-sh") for some predefined functions and variables available in this script.

2) ```openeuler.repo```, reserved repo file, generally used in the -r parameter of build.sh.

3) ```package_conf.xml```, you need to patch the source code repository with git format-patch and configure the software package for source code compilation. An example is given to illustrate the role of each tag.

```
<packages>                                                      <!-- main tag -->
    <package>                                                   <!-- define a package -->
        <name>argon2</name>                                     <!-- package name -->
        <url>https://gitee.com/openeuler-embedded/argon2</url>  <!-- package git repository address -->
        <branch>openEuler-20.03-LTS</branch>                    <!-- repository branch or tag -->
        <patch>../src/patch/argon2.patch</patch>                <!-- path where the git formatpatch format patch is located, the starting point of the path is the path where the configuration file is located -->
        <enabled>1</enabled>                                    <!-- enable source code compilation -->
    </package>                                                  <!-- end a software definition -->
    <package>                                                   <!-- define a package -->
        <name>attr</name>
        <url>https://gitee.com/openeuler-embedded/attr</url>
        <branch>openEuler-20.03-LTS</branch>
        <patch>../src/patch/attr.patch</patch>
        <enabled>1</enabled>
    </package>
    ......
```

#### 4 Example of Using the Image

Take the docker image as an example. The image is located in the image path of the working directory and the name is openEuler-embedded.xxx-xxx.docker.tar.xz.

```shell
docker load -i openEuler-embedded.xxx-xxx.docker.tar.xz
docker run --rm --privileged --name embedded-test -v `pwd`:/data -itd openeuler-embedded init
docker exec -it embedded-test bash
```

#### 5 Environmental Dependence

1）kiwi >= 9.21

2）docker/chroot/createrepo/xmllint/openssl

#### 6 TODO

Up to now, rpm software package compilation and docker image production can be used stably.

To be improved in the next stage:

1) Image diversification support, such as virtual machine image and embedded device image.

2) Scheduling module for rpm building, which can build all software packages based on the automatically identified dependencies.

3) Support cross-compilation

#### 7 Contribution

1.  Fork the repository.
2.  Create Feat_xxx branch.
3.  Commit local code.
4.  Create Pull Request.
