# ha-api

## Introduction
REST API backend for HA manage platform.

Another project is [HA-web](https://gitee.com/openeuler/ha-web), providing frontend UI for HA manage platform. 

## Screenshots

TODO: add some screenshots here

## Features

Easy to use.

## Documents

The following documents are provided to help you understand the project:
 - [Build Document](./docs/build_en.md)
 - [Architecture Document](./docs/architecture_en.md)
 - [API Document](./docs/api_en.md)

## Installation 

HA software is needed to run backend of ha-api manage platform .

In openEuler 20.03 LTS SP1, you can install HA software by yum:

```
[root@ha1~]# yum install corosync pacemaker pcs fence-agents fence-virt corosync-qdevice sbd drbd drbd-utils
```

For another OS, you may need to compile it and then install.
You can get more details in [install documents](./docs/install_en.md) and [build documents](./docs/build_en.md)

## Contribution

HA-api is developed with golang. We use [Beego framework](https://beego.me/) to help us to develop high performance and reliable manage platform. All contributions are welcomed. If you have any problems in using or developing, please contact us by submitting a issue.


## Gitee Feature

1.  You can use Readme\_XXX.md to support different languages, such as Readme\_en.md, Readme\_zh.md
2.  Gitee blog: [blog.gitee.com](https://blog.gitee.com)
3.  You can explore open source project: [https://gitee.com/explore](https://gitee.com/explore)
4.  The Gitee Most Valuable Project ([GVP](https://gitee.com/gvp)),  the excellent open source project comprehensively evaluated by Gitee
5.  The manual of Gitee: [https://gitee.com/help](https://gitee.com/help)
6.  The most popular Gitee members: [https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)

