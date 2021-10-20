# ci-bot

## 产品介绍

ci-bot代码仓库用于处理欧拉开源ci-bot的代码。

## 构架试图

<img src="./docs/images/architecture.png" />

## 先决条件

运行前需安装MySQL数据库，创建数据库实例可参考以下步骤。

* 通过华为云数据库RDS（Relational Database Service）安装MySQL
* 使用账号密码登录MySQL
* 运行下列命令创建数据库实例
    ```
    CREATE DATABASE cibot;
    ```
    数据库实例信息将会在后续安装步骤中使用。

## 配置
### 环境变量
一些机密数据支持从环境变量中读取，您可以在操作系统中设置下列环境变量：

* GITEE_TOKEN 
* WEBHOOK_SECRET
* DATABASE_HOST 
* DATABASE_PORT
* DATABASE_USERNAME
* DATABASE_PASSWORD
### 标签配置
如果您想在Pull Request分支发生变化时清除一些标记，您可以在配置文件（config.yaml）中设置。请见配置文件delLabels字段说明：

 * kind,sig,openeuler-cla,priority。删除以kind、sig、openeuler-cla或priority开头的标签
 * lgtm。删除“lgtm”或以“lgtm”开头的标签
 * 除以上说明项外，其他标签将被视为等同
### extraLgtmCountRequired配置
如果您想为单独的代码仓库或是组织设置lgtm数量，您可以在extraLgtmCountRequired配置中设置。该配置项列表包含了以下配置：

 * lcrType。说明该配置是代码仓库还是组织。 
 * lcrName。配置代码仓库或组织的空间地址。
 * lcrCount。 说明lgtm标签数。

**如果您是为特殊的代码仓库进行配置，您应该配置完整的路径而不只是地址空间。例如 lcrName:openEuler/ci-bot**

## 运行指南

* [本地运行](deploy/locally/README.md)
* [CCE运行](deploy/cce/README.md)

## 命令帮助

英文版请见 [Command Help](https://gitee.com/openeuler/community/blob/master/en/sig-infrastructure/command.md) 。
> 中文版请见 [命令帮助](https://gitee.com/openeuler/community/blob/master/zh/sig-infrastructure/command.md)。

## 许可说明

详见 [许可说明](LICENSE)。

