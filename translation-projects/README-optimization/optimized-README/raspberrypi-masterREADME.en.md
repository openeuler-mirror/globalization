# raspberrypi-build

#### Introduction

Scripts of building images for Raspberry Pi.

#### Software Architecture

AArch64

#### Installation Guidance

There are two approaches to obtain the scripts:

1.  Download the source code of this repository.
2.  You can install raspberrypi-build using `rpm` or `dnf` command based on openEuler 20.09 repository.

    `dnf install raspberrypi-build`

    After installing raspberrypi-build, you can find the scripts and related files for building openEuler image of Raspberry Pi in `/opt/raspberrypi-build`.

#### Usage Guidance

Run the following command to build an image:

`sudo bash build-image.sh -d DIR -r REPO -n IMAGE_NAME`

The meaning of each parameter:

1.  -d, --dir DIR

    Output directory for building images and temporary files, which is the default directory for storing the script. If the `DIR` does not exist, it will be created automatically.

    After the script is executed, the system displays the directory for storing the image. By default, the directory is `DIR/raspi_output/img/`.

2.  -r, --repo REPO_INFO

    Required! The URL/path of target repo file, or the list of repositories' baseurls. Note that if this parameter is a list of baseurls of the repository, use double quotation marks ("") to separate baseurls with spaces.
    
    Examples are as follows:
    
    - The URL of target repo file: *currently unavailable*
    - The path of target repo file: `./openEuler-20.09.repo`

        The content of the repo file is as follows:
        ```
        [OS]
        name=OS
        baseurl=http://119.3.219.20:82/openEuler:/20.09/standard_$basearch/
        enabled=1
        gpgcheck=0

        [EPOL]
        name=EPOL
        baseurl=http://119.3.219.20:82/openEuler:/20.09:/Epol/standard_$basearch/
        enabled=1
        gpgcheck=0
        ```
    - List of repo's baseurls: `"http://119.3.219.20:82/openEuler:/20.09/standard_aarch64/ http://119.3.219.20:82/openEuler:/20.09:/Epol/standard_aarch64/"`

3.  -n, --name IMAGE_NAME

    The image name to be built.
    
    For example, `openEuler-20.09-raspi-aarch64.img`. The default is `openEuler-raspi-aarch64.img`, or it is automatically generated based on parameter: `-n, --name IMAGE_NAME`.

4.  -h, --help
    
    Display help information.

#### Contribution

1.  Fork the repository
2.  Create Feat_xxx branch
3.  Commit your code
4.  Create Pull Request


#### Gitee Feature

1.  You can use Readme\_XXX.md to support different languages, such as Readme\_en.md, Readme\_zh.md
2.  Gitee blog: [blog.gitee.com](https://blog.gitee.com)
3.  Explore open source project at [https://gitee.com/explore](https://gitee.com/explore)
4.  The most valuable open source project is [GVP](https://gitee.com/gvp)
5.  View the manual of Gitee: [https://gitee.com/help](https://gitee.com/help)
6.  Learn about the most popular members: [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)
