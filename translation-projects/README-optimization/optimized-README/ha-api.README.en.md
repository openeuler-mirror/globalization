# ha-api

## Description
REST API backend for HA management platform.

Another relevant project is [HA-web](https://gitee.com/openeuler/ha-web), which provides frontend of HA manage platform. 

## Screenshots

TODO: add some screenshots here

## Features

Easy to use.

## Documents

The following docs may help you know more about the project:
 - [Build Document](./docs/build_en.md)
 - [Architecture Document](./docs/architecture_en.md)
 - [API Document](./docs/api_en.md)

## Install 

HA software is need to run HA management platform backend.

On openEuler 20.03 LTS SP1, you can install HA software by yum:

```
[root@ha1~]# yum install corosync pacemaker pcs fence-agents fence-virt corosync-qdevice sbd drbd drbd-utils
```

For other OSes, you may need to compile it and then install.
You can get more details in [install documents](./docs/install_en.md) and [build documents](./docs/build_en.md)

## Contribution

HA-api is developed with golang. We use [Beego framework](https://beego.me/) to develop high performance and reliable management platform. All contributions are welcomed. If you have any problems in using or developing, please contact us by opening a issue.


## Gitee Feature

1.  You can use Readme\_XXX.md to support different languages, such as Readme\_en.md, Readme\_zh.md
2.  Gitee blog [blog.gitee.com](https://blog.gitee.com)
3.  Explore open source project [https://gitee.com/explore](https://gitee.com/explore)
4.  The most valuable open source project [GVP](https://gitee.com/gvp)
5.  The manual of Gitee [https://gitee.com/help](https://gitee.com/help)
6.  The most popular members https://gitee.com/gitee-stars/](https://gitee.com/gitee-stars/)