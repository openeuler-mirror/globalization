# embedded

#### 1 Introduction

This openEuler version supports embedded devices and currently supports [aarch64|x86_64] CPU architectures 

#### 2 Compilation Instructions

The compilation entry: build.sh

```Usage: 
Usage: 

./build.sh -a [aarch64|x86_64] -r [repo] -d [work dir] -p [live|virtual|disk|docker] -t [rpm|image|all]
```

The role of each parameter is described as follows.

1）-r，specifies the repo file, in the format of the dnf/yum, see [Document 1](https://docs.openeuler.org/zh/docs/20.03_LTS/docs/Administration/%E4%BD%BF%E7%94%A8DNF%E7%AE%A1%E7%90%86%E8%BD%AF%E4%BB%B6%E5%8C%85.html "使用DNF管理软件包").

2）-d，specifies the working directory used in the compilation process, where all intermediate files and the results are stored. As the compilation process requires a large amount of disk space, this directory should be located on a disk with **more than 20G** remaining space.

3）-p，specifies the type of image to be compiled, currently docker image is stably supported.

4）-t，specifies the compilation type, "rpm" means compile the rpm repository according to the source code and patch; "image" means compile the specified image according to the given repo; "all" will execute the compilation process specified by rpm and image in order.

5）-a，no need to specify, set aside parameters to support cross-compilation.

The structure of the working directory (-d specified parameter) during normal compilation is as follows.

```
allsrcpath.list         // list of packages to be compiled according to package_conf.xml
image/                  // the location of image and its description file 
kiwiconfig/
logs_1.tar.gz           // package compilation logs for rounds 1/2 
logs_2.tar.gz           // package compilation logs for rounds 2/2 
openeuler.repo
rpms/                   // the directory where the rpm package is compiled, which can be referenced as a repo source
src/                    // download and patch the package source files according to the configuration file
```

**Note: if the compiled session (login terminal) is prone to disconnections, perform compilation in a manner similar to ```nohup sh build.sh -r ... > log.txt 2>&1 &```** to avoid compilation interruption caused by disconnection.

#### 3 Configuration File Description

The configuration files are located in the config directory：

```
kiwiconf/
openeuler.repo
package_conf.xml
```

1） ```kiwiconf/```，stores the configuration file required for the kiwicompat command. No changes are normally required.

For the format of the config. XML file, see [Document 2](https://documentation.suse.com/kiwi/9/single-html/kiwi/index.html#image-description-elements "image-description-elements"), [Document 3](https://documentation.suse.com/kiwi/9/html/kiwi/image-description.html "image-description").

After creating the system directory kiwi, calls images.sh. This script can be used to trim unnecessary files from the root directory or to make some system settings. Some of the predefined functions and variables to the script are described in [Document 4](https://documentation.suse.com/kiwi/9/single-html/kiwi/index.html#script-template-for-config-sh-images-sh "script-template-for-config-sh-images-sh").

2）```openeuler.repo```，the reserved repo file, generally used in the `-r` parameter of build.sh.

3）```package_conf.xml```，the package configuration that needs to be patched with git format-patch and to be compiled for source code, with an example to illustrate the role of each tag.

```
<packages>                                                      <!-- main tag -->
    <package>                                                   <!-- Define a package -->
        <name>argon2</name>                                     <!-- package name -->
        <url>https://gitee.com/openeuler-embedded/argon2</url>  <!-- package git repository address -->
        <branch>openEuler-20.03-LTS</branch>                    <!-- repository branch or tag -->
        <patch>../src/patch/argon2.patch</patch>                <!-- git formatpatch where the patch is located, the path starts at the path where this configuration file is located -->
        <enabled>1</enabled>                                    <!-- enabled source code compilation -->
    </package>                                                  <!-- end a software definition -->
    <package>                                                   <!-- Define a package -->
        <name>attr</name>
        <url>https://gitee.com/openeuler-embedded/attr</url>
        <branch>openEuler-20.03-LTS</branch>
        <patch>../src/patch/attr.patch</patch>
        <enabled>1</enabled>
    </package>
    ......
```

#### 4 Example of Image Usage

Take the docker image as an example, the image is located in the image path of the working directory named openEuler-embedded.xxx-xxx.docker.tar.xz.

```shell
docker load -i openEuler-embedded.xxx-xxx.docker.tar.xz
docker run --rm --privileged --name embedded-test -v `pwd`:/data -itd openeuler-embedded init
docker exec -it embedded-test bash
```

#### 5 Dependencies

1）kiwi >= 9.21

2）docker/chroot/createrepo/xmllint/openssl

#### 6 TODO

As of now, rpm package compilation and docker image creation is working stably.

Further improve:

1）diversification support, such as virtual machine images and embedded device images, etc.

2）rpm build scheduling module to build all packages correctly based on automatically identified dependencies.

3）cross-compilation support

#### 7 Contributions

1.  Fork this repository
2.  Create a new Feat_xxx branch
3.  Commit code
4.  Create a new Pull Request