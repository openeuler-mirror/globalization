



# openEuler G11N 贡献指南

![image 1](https://gitee.com/yanhuiling/globalization/raw/master/images/image%201.png)

openEuler G11N 特别兴趣小组旨在向全球不同语言背景的openEuler开发者提供专业语言服务平台，向国内开发者普及全球化能力，跨越语言和文化障碍，壮大openEuler社区，使openEuler惠及更多开发者。 

G11N特别兴趣小组欢迎各种形式的贡献，包括但不限于：

- 翻译openEuler社区材料
- 推荐/翻译/撰写热点技术文档或博客
- 修改材料和交付件错误

#### ![image 2](https://gitee.com/yanhuiling/globalization/raw/master/images/image%202.png) 翻译openEuler社区材料

openEuler需要翻译的材料包括官网内容以及开源社区160+仓库的README，about，releases，技术文档等。 若你想为openEuler社区贡献你的译文，请注册Gitee账号并订阅G11N mailing list成为我们小组的一员，然后加入对应语种的翻译团队认领需要翻译的内容。每个语种团队会提供相应的翻译指导，规范、文化禁忌、风格指南、翻译知识库等。

#### ![image 3](https://gitee.com/yanhuiling/globalization/raw/master/images/image%203.png) 推荐/翻译/撰写热点技术文档或博客

分享开源与全球化最新趋势、技术和业界动态。 

- 分享最新动态

整合业界资讯和openEuler最新动态，选取合适内容进行国际化处理（多语转换、排版润色）后进行分享。

- 撰写博客

撰写国际化和OS等主题博客，分享行业洞察和学习收获。

- 推荐或翻译热点技术文档

推荐或翻译热点技术文档，为社区提供全球领域的技术新知识。

#### ![image 4](https://gitee.com/yanhuiling/globalization/raw/master/images/image%204.png) 修改材料和交付件错误

欢迎大家对G11N的材料和交付件进行修改和优化，包括各个仓库的译稿，翻译指导，全球化规范，博客等，只要你发现了不合理/错误的地方，都欢迎提交PR进行修改，让我们一起打造更专业的全球化兴趣小组。

![image 5](https://gitee.com/yanhuiling/globalization/raw/master/images/image%205.png)

以下为具体的贡献指导，请按照步骤操作。

# 一、注册账号并订阅G11N

**步骤 1**:  进入[Gitee主页](https://gitee.com/)注册你的专属账号。

**步骤 2**:  注册成功后登录，点击页面左上角的**个人主页**进入你的个人页面，点击头像下的**个人设置**，再在左边导航栏选择**邮箱管理**，设置一个你的常用邮箱作为主邮箱（这个邮箱非常重要，后面用来接收翻译项目，会议通知等）。 

###### ![image 6](https://gitee.com/yanhuiling/globalization/raw/master/images/image%206.png "image 6")

**步骤 3**:  签署openEuler社区[贡献者许可协议 (CLA)](https://clasign.osinfra.cn/sign/Z2l0ZWUlMkZvcGVuZXVsZXI=) 。请选择**个人CLA**。签署邮箱请填写你设置的主邮箱。

**步骤 4**:  订阅G11N邮件列表。

1. 进入[openEuler社区主页](https://www.openeuler.org/zh/)，选择**社区 > 邮件列表**。

2. 在邮件列表中找到**G11n**并点击进入[订阅页面](https://mailweb.openeuler.org/postorius/lists/g11n.openeuler.org/)。

3. 填写你的名字和主邮箱用于接收G11N消息。

###### <img src="https://gitee.com/yanhuiling/G11N/raw/master/learning-materials/open-source-basics/images/Git%207.PNG" alt="image 7" style="zoom:80%;" />

4. 提交订阅后你的邮箱会收到一个confirm邮件，直接回复邮件进行确认。待收到"Welcome to the "G11n" mailing list"邮件，说明你已订阅成功。

# 二、Markdown和Git工具学习

想要贡献openEuler开源社区，有两个工具需熟练掌握，一个是Typora，一个是Git。

Typora（[下载](https://typora.io/)）：Typora是一个所见即所得的Markdown格式文本编辑器，支持Windows、macOS和GNU/Linux操作系统，包括对GitHub Flavored Markdown扩展格式的支持、拼写检查、自定义CSS样式、数学公式渲染（通过MathJax）等特性。之后我们译稿或博客上传到开源社区需要使用这个格式。具体使用方法，请参考[markdown-basics](待补充链接)。

###### <img src="https://gitee.com/yanhuiling/globalization/raw/master/images/image%209.png" alt="image 9" style="zoom:80%;" />

Git（[下载](https://gitforwindows.org/ )）: Git是一个开源的分布式版本控制系统，可以有效、高速地处理项目版本管理。 我们翻译或创作好的文档需要通过Git工具上传到开源社区。请大家自学一下Git 工具的使用。我们也提供了丰富的学习资源，请参考[git-self-learning-materials](待补充链接)和[git-basics](待补充链接)。

###### ![image 10](https://gitee.com/yanhuiling/globalization/raw/master/images/image%2010.png)

# 三、翻译项目参与流程

###### ![image 11](https://gitee.com/yanhuiling/globalization/raw/master/images/image%2011.png)

上面的准备工作做好后，大家就可以开始参与G11N发布的翻译项目啦。目前试点英文翻译项目，主要流程如下：

- G11N翻译项目协调人员将待翻译任务列表放在G11N/globalization仓库的[translation-projects](https://gitee.com/openeuler/globalization/tree/master/translation-projects)文件夹下，每个翻译任务以“编号-文档名-交付时间”命名并附上对应仓库链接。项目启动时，G11N协调人员会给大家邮箱发布翻译列表，大家根据邮件里的链接或直接进入translation-projects文件夹选取感兴趣的任务发送到G11N邮箱（[g11n@openeuler.org](mailto:g11n@openeuler.org) ）。协调人员收到后会在该任务Translator一栏写上你的ID。有任何问题都可以发邮件到[g11n@openeuler.org](mailto:g11n@openeuler.org)，工作日实时回复。

- 认领好自己的待翻译任务后就可以点击仓库链接去到对应仓库获取待翻译内容。你可以拷贝到线下用word格式进行翻译，方便工具检查和评审，也可以直接用Markdown格式进行编辑。相关翻译风格指南和术语，请参考[xxx](待补充)和xxx。翻译完成后请先自检，保证没有低错、语法错误等。然后发送邮件到G11N邮箱申请评审（请在截稿时间前1-2天发评审，给评审人员预留时间）。评审完成后也会通过邮件返回给你。

- 译稿完成翻译和评审后，你就可以上传到对应仓库，具体方式有两种：轻量级Pull Request（PR）和Git工具上传（需要学习Git工具使用）。

注意：上传的文档必须为Markdown格式，如果你使用word进行翻译，请上传前拷贝到Typora生成Markdown文件。你的译稿除了会上传到对应仓库，G11N协调人员也会将其存档在[translation-projects](https://gitee.com/openeuler/globalization/tree/master/translation-projects)文件夹下。

## 提交轻量级PR

零星变更可以在代码仓（主仓非个人仓）直接修改文档，创建轻量级PR。 这个适用于仓库已有英文版本，且内容相对完整，只需要根据中文进行少量的修改。

**步骤 1**: 根据提供的链接进入对应仓库，找到对应英文文档，单击进入，如图所示。

###### <img src="https://gitee.com/yanhuiling/globalization/raw/master/images/image%2012.png" alt="image 12" style="zoom:80%;" />

**步骤 2**: 点击右上角的**编辑**按钮进入在线编辑模式（Markdown格式）。  

###### <img src="https://gitee.com/yanhuiling/globalization/raw/master/images/image%2013.png" alt="image 13" style="zoom:80%;" />

**步骤 3**: 修改内容并检查完成后预览一下效果，确认无误后在扩展信息内简述变更原因，点击**提交审核**创建一个轻量级PR。若页面跳转到PR详情页面，则轻量级PR创建成功。 审核通过后你的内容就可以合入仓库。

###### <img src="https://gitee.com/yanhuiling/globalization/raw/master/images/image%2014.png" alt="image 14" style="zoom: 67%;" />

## 上传文档到代码仓

流程（使用Git工具操作）

###### ![image 15](https://gitee.com/yanhuiling/globalization/raw/master/images/image%2015.png)

**步骤 1**: 代码仓fork到个人仓。比如点击Fork将[openEuler](https://gitee.com/openeuler) / [globalization](https://gitee.com/openeuler/globalization)仓库fork到你的个人仓。

###### <img src="https://gitee.com/yanhuiling/globalization/raw/master/images/image 16.PNG" alt="image 16" style="zoom: 67%;" />

注意: 上传文档只能先上传到你的个人仓再创建PR推送到主仓进行审核，不能直接上传文件到主仓。待翻译的文档在哪个仓库就fork哪个仓库。比如如果待翻译文档在[openEuler](https://gitee.com/openeuler) / [A-Tune](https://gitee.com/openeuler/A-Tune)仓库，就fork这个仓库到个人仓。

如果之前已经fork到个人仓，此时也可以在个人仓单击同步按钮，将主仓的内容直接同步到个人仓，例如： 

###### <img src="https://gitee.com/yanhuiling/globalization/raw/master/images/image%2017.png" alt="image 17" style="zoom:80%;" />

**步骤 2**：个人仓clone到本地，以克隆[openEuler](https://gitee.com/openeuler) / [globalization](https://gitee.com/openeuler/globalization)仓库为例。

- 如果本地没有个人仓的文件，是首次拉取个人仓文件，请参考下面步骤。 

  1. 新建本地文件夹，以仓库名命名，在文件夹内右键选择“Git Bash Here”，进入Git命令行。Git操作请参考[二、Markdown和Git工具学习](#二、Markdown和Git工具学习)。
  2. 在命令行页面执行**git clone git@gitee.com:yanhuiling/globalization.git**将个人仓的文件拉取到本地。

  ######  <img src="https://gitee.com/yanhuiling/globalization/raw/master/images/image%2018.png" alt="image 18" style="zoom:80%;" />

  其中“git@gitee.com:yanhuiling/globalization.git”为个人仓地址，可以通过如下方式获取：

  ###### <img src="https://gitee.com/yanhuiling/globalization/raw/master/images/image%2019.png" alt="image 19" style="zoom: 67%;" />

  需要注意的是，gitee上默认clone的是master仓的文件，如果需要指定分支，例如clone dev分支的文件，可以通过-b指定，例如：

  **git clone -b dev git@gitee.com:yanhuiling/globalization.git**

- 如果本地已经clone过个人仓的文件，需要更新，则进入本地路径，打开命令行执行**git pull**命令更新本地的文件。 

**步骤 3**：本地push到个人仓。更新本地文档后，运行以下命令提交到个人仓：

```
git add .**

**git commit -m “****变更说明”**

**git push
```

**步骤 4**: 个人仓提交PR到代码仓。在个人仓创建PR。源分支选择个人仓，目的分支选择主仓。分支也要一一对应。审核通过后你的译文便可在仓库呈现。

###### <img src="https://gitee.com/yanhuiling/globalization/raw/master/images/image%2020.png" alt="image 20" style="zoom: 67%;" />

# 四、其他贡献参与流程

#### ![image 3](https://gitee.com/yanhuiling/globalization/raw/master/images/image%203.png) 推荐/翻译/撰写热点技术文档或博客

你可以分享开源与全球化最新趋势、技术和业界动态并撰写博客。 

整合业界资讯和openEuler最新动态，选取合适内容进行国际化处理（多语转换、排版润色）后进行分享。

撰写国际化和OS相关博客，分享行业洞察和学习收获。

推荐或翻译热点技术文档，为社区提供全球领域的技术新知识。

**关键角色**：

- 选题：负责选择合适的内容，并将原文转换为可译格式。
- 译者/作者：负责从选题中选择内容进行翻译/负责编写文章。
- 校对：负责将初译/初写的文章进行文字润色、技术校对等工作。
- 发布：负责将校对后的文章进行排版和发布。

你可以自己担任所有角色，自己选择合适的文章进行翻译或自己选择主题进行撰写，排版好之后通过Git工具上传到[openEuler](https://gitee.com/openeuler) / [globalization](https://gitee.com/openeuler/globalization)仓库的xxx文件夹下。上传方式跟上传译稿一样,请参考[上传文档到代码仓](#上传文档到代码仓)。你也可以选择翻译我们指定的文章或跟我指定主题进行创作，完成后发到G11N 邮箱申请文字润色和技术校对。引用内容请注明出处。文章末尾请附上参与人ID。比如：

- 选题：G11N
- 译者/作者：yan@123
- 校对：hcy@321
- 发布：yan@123

#### ![image 4](https://gitee.com/yanhuiling/globalization/raw/master/images/image%204.png)修改材料和交付件错误

我们欢迎大家对G11N的材料和交付件进行修改和优化，包括各个仓库的译稿，翻译指导，全球化规范，博客等，只要你发现了不合理/错误的地方，都欢迎提交PR进行修改。这种贡献形式比较适合提交轻量级PR，流程请参考[提交轻量级PR](#提交轻量级PR)。



### openEuler G11N期待你的加入~







