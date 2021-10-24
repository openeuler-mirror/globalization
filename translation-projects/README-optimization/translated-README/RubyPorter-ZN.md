# RubyPorter

#### 描述

这是[rubygems.org](rubygems.org)上Ruby模块的RPM打包机器人。使用此机器人，您可以创建**spec**文件并为Ruby模块创建RPM。

#### 准备工作

在使用RubyPorter之前安装以下软件。

* GCC

* GDB

* libstdc++-devel

* ruby-devel

* rubygems-devel

#### 安装

运行**python3 setup.py install**进行安装。

#### 操作

1. 运行**rubyporter -s xxx**来创建一个名为***xxx***的**spec**文件，注意***xxx***应该是RubyGems包中存在的一个工具。运行**-o *yyy***来保存spec记录到***yyy***文件。

```

e、 g.rubyporter-s puma（生成并显示配置记录）

      rubyporter-s puma-o rubygem-puma.spec（保存spec记录到rubygem-puma.spec文件）

```

2. 以***rubyporter-b xxx***的名称构建RPM包。

3. 构建并安装RPM包***rubyporter-B xxx***。

4. 有关更多详细信息，请使用***rubyporter-h***。

#### 贡献

1. Fork此软件仓。

2. 创建**Feat_xxx**分支。

3. 提交代码。

4. 创建PR。

