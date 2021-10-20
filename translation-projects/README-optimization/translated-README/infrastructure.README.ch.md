#  基础架构

### 简介

此库涵盖了社区基础架构的脚本。欢迎加入我们，感谢您的参与和贡献。

###  结构
```
|__environment --house the scripts of basic infrastructure. 
|__mail        --house the scripts of mail list system.
|__website     --house the scripts of CD system.
|__docs        --house the design docs.
|__assets      --house the basic assets, e.g. images.
|__repository  --house the repository maintenance yaml.
|__meetbot     --house the meetbot dockerfile and deployment yaml
```

目前，所有的系统都作为容器在华为云容器引擎CCE 上运行。在此，我们感谢大家为社区贡献自己的基础架构。

### 邮件

我们的邮件列表系统采用的是(Mailman + Exim4 + Postgres)，我们大部分的docker文件都是用maxking](https://github.com/maxking/docker-mailman)和[inifum](https://github.com/infinum/exim4-docker)创建的。

###  会议
- 时间
    北京时间，星期二，17：00-18：00；世界时间，星期二，9：00-10：00

- 频道

    周会将采取IRC的形式，如果你想使用zoom，请提前以邮件列表的形式通知我们。

    频道：https://webchat.freenode.net/#openeuler-meeting

- 会议档案
    网址：http://meetings.openeuler.org/openeuler-meeting/

### 许可证
目前，所有的代码采用apache v2.0许可证。


### 参考

