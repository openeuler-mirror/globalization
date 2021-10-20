# go-gitee

## 介绍

go-gitee是gitee api的go语言工具包。

## 概述
这个API（应用程序编程接口）客户端是由[swagger-codegen](https://github.com/swagger-api/swagger-codegen)项目产生的。通过远程服务器使用[swagger-spec](https://github.com/swagger-api/swagger-spec)，您能轻松地生成一个API客户端。

- API版本: 5.3.2
- 软件包版本: 1.0.0
- 构建软件包: io.swagger.codegen.languages.GoClientCodegen

## API端点文档

所有的统一资源标识符（URI）见链接： *https://gitee.com/api/v5/doc_json*

| 类型               | 方法                                                         | HTTP请求                                                     | 描述                                                    |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------- |
| *ActivityApi*      | [**DeleteV5UserStarredOwnerRepo**](docs/ActivityApi.md#deletev5userstarredownerrepo) | **Delete** /v5/user/starred/{owner}/{repo}                   | 取消 star 一个仓库                                      |
| *ActivityApi*      | [**DeleteV5UserSubscriptionsOwnerRepo**](docs/ActivityApi.md#deletev5usersubscriptionsownerrepo) | **Delete** /v5/user/subscriptions/{owner}/{repo}             | 取消 watch 一个仓库                                     |
| *ActivityApi*      | [**GetV5Events**](docs/ActivityApi.md#getv5events)           | **Get** /v5/events                                           | 获取站内所有公开动态                                    |
| *ActivityApi*      | [**GetV5NetworksOwnerRepoEvents**](docs/ActivityApi.md#getv5networksownerrepoevents) | **Get** /v5/networks/{owner}/{repo}/events                   | 列出仓库的所有公开动态                                  |
| *ActivityApi*      | [**GetV5NotificationsCount**](docs/ActivityApi.md#getv5notificationscount) | **Get** /v5/notifications/count                              | 获取授权用户的通知数                                    |
| *ActivityApi*      | [**GetV5NotificationsMessages**](docs/ActivityApi.md#getv5notificationsmessages) | **Get** /v5/notifications/messages                           | 列出授权用户的所有私信                                  |
| *ActivityApi*      | [**GetV5NotificationsMessagesId**](docs/ActivityApi.md#getv5notificationsmessagesid) | **Get** /v5/notifications/messages/{id}                      | 获取一条私信                                            |
| *ActivityApi*      | [**GetV5NotificationsThreads**](docs/ActivityApi.md#getv5notificationsthreads) | **Get** /v5/notifications/threads                            | 列出授权用户的所有通知                                  |
| *ActivityApi*      | [**GetV5NotificationsThreadsId**](docs/ActivityApi.md#getv5notificationsthreadsid) | **Get** /v5/notifications/threads/{id}                       | 获取一条通知                                            |
| *ActivityApi*      | [**GetV5OrgsOrgEvents**](docs/ActivityApi.md#getv5orgsorgevents) | **Get** /v5/orgs/{org}/events                                | 列出组织的公开动态                                      |
| *ActivityApi*      | [**GetV5ReposOwnerRepoEvents**](docs/ActivityApi.md#getv5reposownerrepoevents) | **Get** /v5/repos/{owner}/{repo}/events                      | 列出仓库的所有动态                                      |
| *ActivityApi*      | [**GetV5ReposOwnerRepoNotifications**](docs/ActivityApi.md#getv5reposownerreponotifications) | **Get** /v5/repos/{owner}/{repo}/notifications               | 列出一个仓库里的通知                                    |
| *ActivityApi*      | [**GetV5ReposOwnerRepoStargazers**](docs/ActivityApi.md#getv5reposownerrepostargazers) | **Get** /v5/repos/{owner}/{repo}/stargazers                  | 列出 star 了仓库的用户                                  |
| *ActivityApi*      | [**GetV5ReposOwnerRepoSubscribers**](docs/ActivityApi.md#getv5reposownerreposubscribers) | **Get** /v5/repos/{owner}/{repo}/subscribers                 | 列出 watch 了仓库的用户                                 |
| *ActivityApi*      | [**GetV5UserStarred**](docs/ActivityApi.md#getv5userstarred) | **Get** /v5/user/starred                                     | 列出授权用户 star 了的仓库                              |
| *ActivityApi*      | [**GetV5UserStarredOwnerRepo**](docs/ActivityApi.md#getv5userstarredownerrepo) | **Get** /v5/user/starred/{owner}/{repo}                      | 检查授权用户是否 star 了一个仓库                        |
| *ActivityApi*      | [**GetV5UserSubscriptions**](docs/ActivityApi.md#getv5usersubscriptions) | **Get** /v5/user/subscriptions                               | 列出授权用户 watch 了的仓库                             |
| *ActivityApi*      | [**GetV5UserSubscriptionsOwnerRepo**](docs/ActivityApi.md#getv5usersubscriptionsownerrepo) | **Get** /v5/user/subscriptions/{owner}/{repo}                | 检查授权用户是否 watch 了一个仓库                       |
| *ActivityApi*      | [**GetV5UsersUsernameEvents**](docs/ActivityApi.md#getv5usersusernameevents) | **Get** /v5/users/{username}/events                          | 列出用户的动态                                          |
| *ActivityApi*      | [**GetV5UsersUsernameEventsOrgsOrg**](docs/ActivityApi.md#getv5usersusernameeventsorgsorg) | **Get** /v5/users/{username}/events/orgs/{org}               | 列出用户所属组织的动态                                  |
| *ActivityApi*      | [**GetV5UsersUsernameEventsPublic**](docs/ActivityApi.md#getv5usersusernameeventspublic) | **Get** /v5/users/{username}/events/public                   | 列出用户的公开动态                                      |
| *ActivityApi*      | [**GetV5UsersUsernameReceivedEvents**](docs/ActivityApi.md#getv5usersusernamereceivedevents) | **Get** /v5/users/{username}/received_events                 | 列出一个用户收到的动态                                  |
| *ActivityApi*      | [**GetV5UsersUsernameReceivedEventsPublic**](docs/ActivityApi.md#getv5usersusernamereceivedeventspublic) | **Get** /v5/users/{username}/received_events/public          | 列出一个用户收到的公开动态                              |
| *ActivityApi*      | [**GetV5UsersUsernameStarred**](docs/ActivityApi.md#getv5usersusernamestarred) | **Get** /v5/users/{username}/starred                         | 列出用户 star 了的仓库                                  |
| *ActivityApi*      | [**GetV5UsersUsernameSubscriptions**](docs/ActivityApi.md#getv5usersusernamesubscriptions) | **Get** /v5/users/{username}/subscriptions                   | 列出用户 watch 了的仓库                                 |
| *ActivityApi*      | [**PatchV5NotificationsMessagesId**](docs/ActivityApi.md#patchv5notificationsmessagesid) | **Patch** /v5/notifications/messages/{id}                    | 标记一条私信为已读                                      |
| *ActivityApi*      | [**PatchV5NotificationsThreadsId**](docs/ActivityApi.md#patchv5notificationsthreadsid) | **Patch** /v5/notifications/threads/{id}                     | 标记一条通知为已读                                      |
| *ActivityApi*      | [**PostV5NotificationsMessages**](docs/ActivityApi.md#postv5notificationsmessages) | **Post** /v5/notifications/messages                          | 发送私信给指定用户                                      |
| *ActivityApi*      | [**PutV5NotificationsMessages**](docs/ActivityApi.md#putv5notificationsmessages) | **Put** /v5/notifications/messages                           | 标记所有私信为已读                                      |
| *ActivityApi*      | [**PutV5NotificationsThreads**](docs/ActivityApi.md#putv5notificationsthreads) | **Put** /v5/notifications/threads                            | 标记所有通知为已读                                      |
| *ActivityApi*      | [**PutV5ReposOwnerRepoNotifications**](docs/ActivityApi.md#putv5reposownerreponotifications) | **Put** /v5/repos/{owner}/{repo}/notifications               | 标记一个仓库里的通知为已读                              |
| *ActivityApi*      | [**PutV5UserStarredOwnerRepo**](docs/ActivityApi.md#putv5userstarredownerrepo) | **Put** /v5/user/starred/{owner}/{repo}                      | star 一个仓库                                           |
| *ActivityApi*      | [**PutV5UserSubscriptionsOwnerRepo**](docs/ActivityApi.md#putv5usersubscriptionsownerrepo) | **Put** /v5/user/subscriptions/{owner}/{repo}                | watch 一个仓库                                          |
| *EmailsApi*        | [**GetV5Emails**](docs/EmailsApi.md#getv5emails)             | **Get** /v5/emails                                           | 获取授权用户的所有邮箱                                  |
| *EnterprisesApi*   | [**DeleteV5EnterprisesEnterpriseMembersUsername**](docs/EnterprisesApi.md#deletev5enterprisesenterprisemembersusername) | **Delete** /v5/enterprises/{enterprise}/members/{username}   | 移除企业成员                                            |
| *EnterprisesApi*   | [**DeleteV5EnterprisesEnterpriseWeekReportsReportIdCommentsId**](docs/EnterprisesApi.md#deletev5enterprisesenterpriseweekreportsreportidcommentsid) | **Delete** /v5/enterprises/{enterprise}/week_reports/{report_id}/comments/{id} | 删除周报某个评论                                        |
| *EnterprisesApi*   | [**GetV5EnterprisesEnterprise**](docs/EnterprisesApi.md#getv5enterprisesenterprise) | **Get** /v5/enterprises/{enterprise}                         | 获取一个企业                                            |
| *EnterprisesApi*   | [**GetV5EnterprisesEnterpriseMembers**](docs/EnterprisesApi.md#getv5enterprisesenterprisemembers) | **Get** /v5/enterprises/{enterprise}/members                 | 列出企业的所有成员                                      |
| *EnterprisesApi*   | [**GetV5EnterprisesEnterpriseMembersUsername**](docs/EnterprisesApi.md#getv5enterprisesenterprisemembersusername) | **Get** /v5/enterprises/{enterprise}/members/{username}      | 获取企业的一个成员                                      |
| *EnterprisesApi*   | [**GetV5EnterprisesEnterpriseUsersUsernameWeekReports**](docs/EnterprisesApi.md#getv5enterprisesenterpriseusersusernameweekreports) | **Get** /v5/enterprises/{enterprise}/users/{username}/week_reports | 个人周报列表                                            |
| *EnterprisesApi*   | [**GetV5EnterprisesEnterpriseWeekReports**](docs/EnterprisesApi.md#getv5enterprisesenterpriseweekreports) | **Get** /v5/enterprises/{enterprise}/week_reports            | 企业成员周报列表                                        |
| *EnterprisesApi*   | [**GetV5EnterprisesEnterpriseWeekReportsId**](docs/EnterprisesApi.md#getv5enterprisesenterpriseweekreportsid) | **Get** /v5/enterprises/{enterprise}/week_reports/{id}       | 周报详情                                                |
| *EnterprisesApi*   | [**GetV5EnterprisesEnterpriseWeekReportsIdComments**](docs/EnterprisesApi.md#getv5enterprisesenterpriseweekreportsidcomments) | **Get** /v5/enterprises/{enterprise}/week_reports/{id}/comments | 某个周报评论列表                                        |
| *EnterprisesApi*   | [**GetV5UserEnterprises**](docs/EnterprisesApi.md#getv5userenterprises) | **Get** /v5/user/enterprises                                 | 列出授权用户所属的企业                                  |
| *EnterprisesApi*   | [**PatchV5EnterprisesEnterpriseWeekReportId**](docs/EnterprisesApi.md#patchv5enterprisesenterpriseweekreportid) | **Patch** /v5/enterprises/{enterprise}/week_report/{id}      | 编辑周报                                                |
| *EnterprisesApi*   | [**PostV5EnterprisesEnterpriseMembers**](docs/EnterprisesApi.md#postv5enterprisesenterprisemembers) | **Post** /v5/enterprises/{enterprise}/members                | 添加或邀请企业成员                                      |
| *EnterprisesApi*   | [**PostV5EnterprisesEnterpriseWeekReport**](docs/EnterprisesApi.md#postv5enterprisesenterpriseweekreport) | **Post** /v5/enterprises/{enterprise}/week_report            | 新建周报                                                |
| *EnterprisesApi*   | [**PostV5EnterprisesEnterpriseWeekReportsIdComment**](docs/EnterprisesApi.md#postv5enterprisesenterpriseweekreportsidcomment) | **Post** /v5/enterprises/{enterprise}/week_reports/{id}/comment | 评论周报                                                |
| *EnterprisesApi*   | [**PutV5EnterprisesEnterpriseMembersUsername**](docs/EnterprisesApi.md#putv5enterprisesenterprisemembersusername) | **Put** /v5/enterprises/{enterprise}/members/{username}      | 修改企业成员权限或备注                                  |
| *GistsApi*         | [**DeleteV5GistsGistIdCommentsId**](docs/GistsApi.md#deletev5gistsgistidcommentsid) | **Delete** /v5/gists/{gist_id}/comments/{id}                 | 删除代码片段的评论                                      |
| *GistsApi*         | [**DeleteV5GistsId**](docs/GistsApi.md#deletev5gistsid)      | **Delete** /v5/gists/{id}                                    | 删除指定代码片段                                        |
| *GistsApi*         | [**DeleteV5GistsIdStar**](docs/GistsApi.md#deletev5gistsidstar) | **Delete** /v5/gists/{id}/star                               | 取消Star代码片段                                        |
| *GistsApi*         | [**GetV5Gists**](docs/GistsApi.md#getv5gists)                | **Get** /v5/gists                                            | 获取代码片段                                            |
| *GistsApi*         | [**GetV5GistsGistIdComments**](docs/GistsApi.md#getv5gistsgistidcomments) | **Get** /v5/gists/{gist_id}/comments                         | 获取代码片段的评论                                      |
| *GistsApi*         | [**GetV5GistsGistIdCommentsId**](docs/GistsApi.md#getv5gistsgistidcommentsid) | **Get** /v5/gists/{gist_id}/comments/{id}                    | 获取单条代码片段的评论                                  |
| *GistsApi*         | [**GetV5GistsId**](docs/GistsApi.md#getv5gistsid)            | **Get** /v5/gists/{id}                                       | 获取单条代码片段                                        |
| *GistsApi*         | [**GetV5GistsIdCommits**](docs/GistsApi.md#getv5gistsidcommits) | **Get** /v5/gists/{id}/commits                               | 获取代码片段的commit                                    |
| *GistsApi*         | [**GetV5GistsIdForks**](docs/GistsApi.md#getv5gistsidforks)  | **Get** /v5/gists/{id}/forks                                 | 获取 Fork 了指定代码片段的列表                          |
| *GistsApi*         | [**GetV5GistsIdStar**](docs/GistsApi.md#getv5gistsidstar)    | **Get** /v5/gists/{id}/star                                  | 判断代码片段是否已Star                                  |
| *GistsApi*         | [**GetV5GistsPublic**](docs/GistsApi.md#getv5gistspublic)    | **Get** /v5/gists/public                                     | 获取公开的代码片段                                      |
| *GistsApi*         | [**GetV5GistsStarred**](docs/GistsApi.md#getv5gistsstarred)  | **Get** /v5/gists/starred                                    | 获取用户Star的代码片段                                  |
| *GistsApi*         | [**GetV5UsersUsernameGists**](docs/GistsApi.md#getv5usersusernamegists) | **Get** /v5/users/{username}/gists                           | 获取指定用户的公开代码片段                              |
| *GistsApi*         | [**PatchV5GistsGistIdCommentsId**](docs/GistsApi.md#patchv5gistsgistidcommentsid) | **Patch** /v5/gists/{gist_id}/comments/{id}                  | 修改代码片段的评论                                      |
| *GistsApi*         | [**PatchV5GistsId**](docs/GistsApi.md#patchv5gistsid)        | **Patch** /v5/gists/{id}                                     | 修改代码片段                                            |
| *GistsApi*         | [**PostV5Gists**](docs/GistsApi.md#postv5gists)              | **Post** /v5/gists                                           | 创建代码片段                                            |
| *GistsApi*         | [**PostV5GistsGistIdComments**](docs/GistsApi.md#postv5gistsgistidcomments) | **Post** /v5/gists/{gist_id}/comments                        | 增加代码片段的评论                                      |
| *GistsApi*         | [**PostV5GistsIdForks**](docs/GistsApi.md#postv5gistsidforks) | **Post** /v5/gists/{id}/forks                                | Fork代码片段                                            |
| *GistsApi*         | [**PutV5GistsIdStar**](docs/GistsApi.md#putv5gistsidstar)    | **Put** /v5/gists/{id}/star                                  | Star代码片段                                            |
| *GitDataApi*       | [**GetV5ReposOwnerRepoGitBlobsSha**](docs/GitDataApi.md#getv5reposownerrepogitblobssha) | **Get** /v5/repos/{owner}/{repo}/git/blobs/{sha}             | 获取文件Blob                                            |
| *GitDataApi*       | [**GetV5ReposOwnerRepoGitTreesSha**](docs/GitDataApi.md#getv5reposownerrepogittreessha) | **Get** /v5/repos/{owner}/{repo}/git/trees/{sha}             | 获取目录Tree                                            |
| *IssuesApi*        | [**DeleteV5ReposOwnerRepoIssuesCommentsId**](docs/IssuesApi.md#deletev5reposownerrepoissuescommentsid) | **Delete** /v5/repos/{owner}/{repo}/issues/comments/{id}     | 删除Issue某条评论                                       |
| *IssuesApi*        | [**GetV5EnterprisesEnterpriseIssues**](docs/IssuesApi.md#getv5enterprisesenterpriseissues) | **Get** /v5/enterprises/{enterprise}/issues                  | 获取某个企业的所有Issues                                |
| *IssuesApi*        | [**GetV5EnterprisesEnterpriseIssuesNumber**](docs/IssuesApi.md#getv5enterprisesenterpriseissuesnumber) | **Get** /v5/enterprises/{enterprise}/issues/{number}         | 获取企业的某个Issue                                     |
| *IssuesApi*        | [**GetV5EnterprisesEnterpriseIssuesNumberComments**](docs/IssuesApi.md#getv5enterprisesenterpriseissuesnumbercomments) | **Get** /v5/enterprises/{enterprise}/issues/{number}/comments | 获取企业某个Issue所有评论                               |
| *IssuesApi*        | [**GetV5EnterprisesEnterpriseIssuesNumberLabels**](docs/IssuesApi.md#getv5enterprisesenterpriseissuesnumberlabels) | **Get** /v5/enterprises/{enterprise}/issues/{number}/labels  | 获取企业某个Issue所有标签                               |
| *IssuesApi*        | [**GetV5Issues**](docs/IssuesApi.md#getv5issues)             | **Get** /v5/issues                                           | 获取当前授权用户的所有Issues                            |
| *IssuesApi*        | [**GetV5OrgsOrgIssues**](docs/IssuesApi.md#getv5orgsorgissues) | **Get** /v5/orgs/{org}/issues                                | 获取当前用户某个组织的Issues                            |
| *IssuesApi*        | [**GetV5ReposOwnerIssuesNumberOperateLogs**](docs/IssuesApi.md#getv5reposownerissuesnumberoperatelogs) | **Get** /v5/repos/{owner}/issues/{number}/operate_logs       | 获取某个Issue下的操作日志                               |
| *IssuesApi*        | [**GetV5ReposOwnerRepoIssues**](docs/IssuesApi.md#getv5reposownerrepoissues) | **Get** /v5/repos/{owner}/{repo}/issues                      | 仓库的所有Issues                                        |
| *IssuesApi*        | [**GetV5ReposOwnerRepoIssuesComments**](docs/IssuesApi.md#getv5reposownerrepoissuescomments) | **Get** /v5/repos/{owner}/{repo}/issues/comments             | 获取仓库所有Issue的评论                                 |
| *IssuesApi*        | [**GetV5ReposOwnerRepoIssuesCommentsId**](docs/IssuesApi.md#getv5reposownerrepoissuescommentsid) | **Get** /v5/repos/{owner}/{repo}/issues/comments/{id}        | 获取仓库Issue某条评论                                   |
| *IssuesApi*        | [**GetV5ReposOwnerRepoIssuesNumber**](docs/IssuesApi.md#getv5reposownerrepoissuesnumber) | **Get** /v5/repos/{owner}/{repo}/issues/{number}             | 仓库的某个Issue                                         |
| *IssuesApi*        | [**GetV5ReposOwnerRepoIssuesNumberComments**](docs/IssuesApi.md#getv5reposownerrepoissuesnumbercomments) | **Get** /v5/repos/{owner}/{repo}/issues/{number}/comments    | 获取仓库某个Issue所有的评论                             |
| *IssuesApi*        | [**GetV5UserIssues**](docs/IssuesApi.md#getv5userissues)     | **Get** /v5/user/issues                                      | 获取授权用户的所有Issues                                |
| *IssuesApi*        | [**PatchV5ReposOwnerIssuesNumber**](docs/IssuesApi.md#patchv5reposownerissuesnumber) | **Patch** /v5/repos/{owner}/issues/{number}                  | 更新Issue                                               |
| *IssuesApi*        | [**PatchV5ReposOwnerRepoIssuesCommentsId**](docs/IssuesApi.md#patchv5reposownerrepoissuescommentsid) | **Patch** /v5/repos/{owner}/{repo}/issues/comments/{id}      | 更新Issue某条评论                                       |
| *IssuesApi*        | [**PostV5ReposOwnerIssues**](docs/IssuesApi.md#postv5reposownerissues) | **Post** /v5/repos/{owner}/issues                            | 创建Issue                                               |
| *IssuesApi*        | [**PostV5ReposOwnerRepoIssuesNumberComments**](docs/IssuesApi.md#postv5reposownerrepoissuesnumbercomments) | **Post** /v5/repos/{owner}/{repo}/issues/{number}/comments   | 创建某个Issue评论                                       |
| *LabelsApi*        | [**DeleteV5ReposOwnerRepoIssuesNumberLabels**](docs/LabelsApi.md#deletev5reposownerrepoissuesnumberlabels) | **Delete** /v5/repos/{owner}/{repo}/issues/{number}/labels   | 删除Issue所有标签                                       |
| *LabelsApi*        | [**DeleteV5ReposOwnerRepoIssuesNumberLabelsName**](docs/LabelsApi.md#deletev5reposownerrepoissuesnumberlabelsname) | **Delete** /v5/repos/{owner}/{repo}/issues/{number}/labels/{name} | 删除Issue标签                                           |
| *LabelsApi*        | [**DeleteV5ReposOwnerRepoLabelsName**](docs/LabelsApi.md#deletev5reposownerrepolabelsname) | **Delete** /v5/repos/{owner}/{repo}/labels/{name}            | 删除一个仓库任务标签                                    |
| *LabelsApi*        | [**GetV5EnterprisesEnterpriseLabels**](docs/LabelsApi.md#getv5enterprisesenterpriselabels) | **Get** /v5/enterprises/{enterprise}/labels                  | 获取企业所有标签                                        |
| *LabelsApi*        | [**GetV5EnterprisesEnterpriseLabelsName**](docs/LabelsApi.md#getv5enterprisesenterpriselabelsname) | **Get** /v5/enterprises/{enterprise}/labels/{name}           | 获取企业某个标签                                        |
| *LabelsApi*        | [**GetV5ReposOwnerRepoIssuesNumberLabels**](docs/LabelsApi.md#getv5reposownerrepoissuesnumberlabels) | **Get** /v5/repos/{owner}/{repo}/issues/{number}/labels      | 获取仓库任务的所有标签                                  |
| *LabelsApi*        | [**GetV5ReposOwnerRepoLabels**](docs/LabelsApi.md#getv5reposownerrepolabels) | **Get** /v5/repos/{owner}/{repo}/labels                      | 获取仓库所有任务标签                                    |
| *LabelsApi*        | [**GetV5ReposOwnerRepoLabelsName**](docs/LabelsApi.md#getv5reposownerrepolabelsname) | **Get** /v5/repos/{owner}/{repo}/labels/{name}               | 根据标签名称获取单个标签                                |
| *LabelsApi*        | [**PatchV5ReposOwnerRepoLabelsOriginalName**](docs/LabelsApi.md#patchv5reposownerrepolabelsoriginalname) | **Patch** /v5/repos/{owner}/{repo}/labels/{original_name}    | 更新一个仓库任务标签                                    |
| *LabelsApi*        | [**PostV5ReposOwnerRepoIssuesNumberLabels**](docs/LabelsApi.md#postv5reposownerrepoissuesnumberlabels) | **Post** /v5/repos/{owner}/{repo}/issues/{number}/labels     | 创建Issue标签                                           |
| *LabelsApi*        | [**PostV5ReposOwnerRepoLabels**](docs/LabelsApi.md#postv5reposownerrepolabels) | **Post** /v5/repos/{owner}/{repo}/labels                     | 创建仓库任务标签                                        |
| *LabelsApi*        | [**PutV5ReposOwnerRepoIssuesNumberLabels**](docs/LabelsApi.md#putv5reposownerrepoissuesnumberlabels) | **Put** /v5/repos/{owner}/{repo}/issues/{number}/labels      | 替换Issue所有标签                                       |
| *MilestonesApi*    | [**DeleteV5ReposOwnerRepoMilestonesNumber**](docs/MilestonesApi.md#deletev5reposownerrepomilestonesnumber) | **Delete** /v5/repos/{owner}/{repo}/milestones/{number}      | 删除仓库单个里程碑                                      |
| *MilestonesApi*    | [**GetV5ReposOwnerRepoMilestones**](docs/MilestonesApi.md#getv5reposownerrepomilestones) | **Get** /v5/repos/{owner}/{repo}/milestones                  | 获取仓库所有里程碑                                      |
| *MilestonesApi*    | [**GetV5ReposOwnerRepoMilestonesNumber**](docs/MilestonesApi.md#getv5reposownerrepomilestonesnumber) | **Get** /v5/repos/{owner}/{repo}/milestones/{number}         | 获取仓库单个里程碑                                      |
| *MilestonesApi*    | [**PatchV5ReposOwnerRepoMilestonesNumber**](docs/MilestonesApi.md#patchv5reposownerrepomilestonesnumber) | **Patch** /v5/repos/{owner}/{repo}/milestones/{number}       | 更新仓库里程碑                                          |
| *MilestonesApi*    | [**PostV5ReposOwnerRepoMilestones**](docs/MilestonesApi.md#postv5reposownerrepomilestones) | **Post** /v5/repos/{owner}/{repo}/milestones                 | 创建仓库里程碑                                          |
| *MiscellaneousApi* | [**GetV5Emojis**](docs/MiscellaneousApi.md#getv5emojis)      | **Get** /v5/emojis                                           | 列出可使用的 Emoji                                      |
| *MiscellaneousApi* | [**GetV5GitignoreTemplates**](docs/MiscellaneousApi.md#getv5gitignoretemplates) | **Get** /v5/gitignore/templates                              | 列出可使用的 .gitignore 模板                            |
| *MiscellaneousApi* | [**GetV5GitignoreTemplatesName**](docs/MiscellaneousApi.md#getv5gitignoretemplatesname) | **Get** /v5/gitignore/templates/{name}                       | 获取一个 .gitignore 模板                                |
| *MiscellaneousApi* | [**GetV5GitignoreTemplatesNameRaw**](docs/MiscellaneousApi.md#getv5gitignoretemplatesnameraw) | **Get** /v5/gitignore/templates/{name}/raw                   | 获取一个 .gitignore 模板原始文件                        |
| *MiscellaneousApi* | [**GetV5Licenses**](docs/MiscellaneousApi.md#getv5licenses)  | **Get** /v5/licenses                                         | 列出可使用的开源许可协议                                |
| *MiscellaneousApi* | [**GetV5LicensesLicense**](docs/MiscellaneousApi.md#getv5licenseslicense) | **Get** /v5/licenses/{license}                               | 获取一个开源许可协议                                    |
| *MiscellaneousApi* | [**GetV5LicensesLicenseRaw**](docs/MiscellaneousApi.md#getv5licenseslicenseraw) | **Get** /v5/licenses/{license}/raw                           | 获取一个开源许可协议原始文件                            |
| *MiscellaneousApi* | [**GetV5ReposOwnerRepoLicense**](docs/MiscellaneousApi.md#getv5reposownerrepolicense) | **Get** /v5/repos/{owner}/{repo}/license                     | 获取一个仓库使用的开源许可协议                          |
| *MiscellaneousApi* | [**PostV5Markdown**](docs/MiscellaneousApi.md#postv5markdown) | **Post** /v5/markdown                                        | 渲染 Markdown 文本                                      |
| *OrganizationsApi* | [**DeleteV5OrgsOrgMembershipsUsername**](docs/OrganizationsApi.md#deletev5orgsorgmembershipsusername) | **Delete** /v5/orgs/{org}/memberships/{username}             | 移除授权用户所管理组织中的成员                          |
| *OrganizationsApi* | [**DeleteV5UserMembershipsOrgsOrg**](docs/OrganizationsApi.md#deletev5usermembershipsorgsorg) | **Delete** /v5/user/memberships/orgs/{org}                   | 退出一个组织                                            |
| *OrganizationsApi* | [**GetV5OrgsOrg**](docs/OrganizationsApi.md#getv5orgsorg)    | **Get** /v5/orgs/{org}                                       | 获取一个组织                                            |
| *OrganizationsApi* | [**GetV5OrgsOrgMembers**](docs/OrganizationsApi.md#getv5orgsorgmembers) | **Get** /v5/orgs/{org}/members                               | 列出一个组织的所有成员                                  |
| *OrganizationsApi* | [**GetV5OrgsOrgMembershipsUsername**](docs/OrganizationsApi.md#getv5orgsorgmembershipsusername) | **Get** /v5/orgs/{org}/memberships/{username}                | 获取授权用户所属组织的一个成员                          |
| *OrganizationsApi* | [**GetV5UserMembershipsOrgs**](docs/OrganizationsApi.md#getv5usermembershipsorgs) | **Get** /v5/user/memberships/orgs                            | 列出授权用户在所属组织的成员资料                        |
| *OrganizationsApi* | [**GetV5UserMembershipsOrgsOrg**](docs/OrganizationsApi.md#getv5usermembershipsorgsorg) | **Get** /v5/user/memberships/orgs/{org}                      | 获取授权用户在一个组织的成员资料                        |
| *OrganizationsApi* | [**GetV5UserOrgs**](docs/OrganizationsApi.md#getv5userorgs)  | **Get** /v5/user/orgs                                        | 列出授权用户所属的组织                                  |
| *OrganizationsApi* | [**GetV5UsersUsernameOrgs**](docs/OrganizationsApi.md#getv5usersusernameorgs) | **Get** /v5/users/{username}/orgs                            | 列出用户所属的组织                                      |
| *OrganizationsApi* | [**PatchV5OrgsOrg**](docs/OrganizationsApi.md#patchv5orgsorg) | **Patch** /v5/orgs/{org}                                     | 更新授权用户所管理的组织资料                            |
| *OrganizationsApi* | [**PatchV5UserMembershipsOrgsOrg**](docs/OrganizationsApi.md#patchv5usermembershipsorgsorg) | **Patch** /v5/user/memberships/orgs/{org}                    | 更新授权用户在一个组织的成员资料                        |
| *OrganizationsApi* | [**PostV5UsersOrganization**](docs/OrganizationsApi.md#postv5usersorganization) | **Post** /v5/users/organization                              | 创建组织                                                |
| *OrganizationsApi* | [**PutV5OrgsOrgMembershipsUsername**](docs/OrganizationsApi.md#putv5orgsorgmembershipsusername) | **Put** /v5/orgs/{org}/memberships/{username}                | 增加或更新授权用户所管理组织的成员                      |
| *PullRequestsApi*  | [**DeleteV5ReposOwnerRepoPullsCommentsId**](docs/PullRequestsApi.md#deletev5reposownerrepopullscommentsid) | **Delete** /v5/repos/{owner}/{repo}/pulls/comments/{id}      | 删除评论                                                |
| *PullRequestsApi*  | [**DeleteV5ReposOwnerRepoPullsLabel**](docs/PullRequestsApi.md#deletev5reposownerrepopullslabel) | **Delete** /v5/repos/{owner}/{repo}/pulls/{number}/labels/{name} | 删除 Pull Request 标签                                  |
| *PullRequestsApi*  | [**DeleteV5ReposOwnerRepoPullsNumberAssignees**](docs/PullRequestsApi.md#deletev5reposownerrepopullsnumberassignees) | **Delete** /v5/repos/{owner}/{repo}/pulls/{number}/assignees | 取消用户审查 Pull Request                               |
| *PullRequestsApi*  | [**DeleteV5ReposOwnerRepoPullsNumberTesters**](docs/PullRequestsApi.md#deletev5reposownerrepopullsnumbertesters) | **Delete** /v5/repos/{owner}/{repo}/pulls/{number}/testers   | 取消用户测试 Pull Request                               |
| *PullRequestsApi*  | [**GetV5ReposOwnerRepoPulls**](docs/PullRequestsApi.md#getv5reposownerrepopulls) | **Get** /v5/repos/{owner}/{repo}/pulls                       | 获取Pull Request列表                                    |
| *PullRequestsApi*  | [**GetV5ReposOwnerRepoPullsComments**](docs/PullRequestsApi.md#getv5reposownerrepopullscomments) | **Get** /v5/repos/{owner}/{repo}/pulls/comments              | 获取该仓库下的所有Pull Request评论                      |
| *PullRequestsApi*  | [**GetV5ReposOwnerRepoPullsCommentsId**](docs/PullRequestsApi.md#getv5reposownerrepopullscommentsid) | **Get** /v5/repos/{owner}/{repo}/pulls/comments/{id}         | 获取Pull Request的某个评论                              |
| *PullRequestsApi*  | [**GetV5ReposOwnerRepoPullsNumber**](docs/PullRequestsApi.md#getv5reposownerrepopullsnumber) | **Get** /v5/repos/{owner}/{repo}/pulls/{number}              | 获取单个Pull Request                                    |
| *PullRequestsApi*  | [**GetV5ReposOwnerRepoPullsNumberComments**](docs/PullRequestsApi.md#getv5reposownerrepopullsnumbercomments) | **Get** /v5/repos/{owner}/{repo}/pulls/{number}/comments     | 获取某个Pull Request的所有评论                          |
| *PullRequestsApi*  | [**GetV5ReposOwnerRepoPullsNumberCommits**](docs/PullRequestsApi.md#getv5reposownerrepopullsnumbercommits) | **Get** /v5/repos/{owner}/{repo}/pulls/{number}/commits      | 获取某Pull Request的所有Commit信息。最多显示250条Commit |
| *PullRequestsApi*  | [**GetV5ReposOwnerRepoPullsNumberFiles**](docs/PullRequestsApi.md#getv5reposownerrepopullsnumberfiles) | **Get** /v5/repos/{owner}/{repo}/pulls/{number}/files        | Pull Request Commit文件列表。最多显示300条diff          |
| *PullRequestsApi*  | [**GetV5ReposOwnerRepoPullsNumberIssues**](docs/PullRequestsApi.md#getv5reposownerrepopullsnumberissues) | **Get** /v5/repos/{owner}/{repo}/pulls/{number}/issues       | 获取 Pull Request 关联的 issues                         |
| *PullRequestsApi*  | [**GetV5ReposOwnerRepoPullsNumberLabels**](docs/PullRequestsApi.md#getv5reposownerrepopullsnumberlabels) | **Get** /v5/repos/{owner}/{repo}/pulls/{number}/labels       | 获取某个 Pull Request 的所有标签                        |
| *PullRequestsApi*  | [**GetV5ReposOwnerRepoPullsNumberMerge**](docs/PullRequestsApi.md#getv5reposownerrepopullsnumbermerge) | **Get** /v5/repos/{owner}/{repo}/pulls/{number}/merge        | 判断Pull Request是否已经合并                            |
| *PullRequestsApi*  | [**GetV5ReposOwnerRepoPullsNumberOperateLogs**](docs/PullRequestsApi.md#getv5reposownerrepopullsnumberoperatelogs) | **Get** /v5/repos/{owner}/{repo}/pulls/{number}/operate_logs | 获取某个Pull Request的操作日志                          |
| *PullRequestsApi*  | [**PatchV5ReposOwnerRepoPullsCommentsId**](docs/PullRequestsApi.md#patchv5reposownerrepopullscommentsid) | **Patch** /v5/repos/{owner}/{repo}/pulls/comments/{id}       | 编辑评论                                                |
| *PullRequestsApi*  | [**PatchV5ReposOwnerRepoPullsNumber**](docs/PullRequestsApi.md#patchv5reposownerrepopullsnumber) | **Patch** /v5/repos/{owner}/{repo}/pulls/{number}            | 更新Pull Request信息                                    |
| *PullRequestsApi*  | [**PostV5ReposOwnerRepoPulls**](docs/PullRequestsApi.md#postv5reposownerrepopulls) | **Post** /v5/repos/{owner}/{repo}/pulls                      | 创建Pull Request                                        |
| *PullRequestsApi*  | [**PostV5ReposOwnerRepoPullsNumberAssignees**](docs/PullRequestsApi.md#postv5reposownerrepopullsnumberassignees) | **Post** /v5/repos/{owner}/{repo}/pulls/{number}/assignees   | 指派用户审查 Pull Request                               |
| *PullRequestsApi*  | [**PostV5ReposOwnerRepoPullsNumberComments**](docs/PullRequestsApi.md#postv5reposownerrepopullsnumbercomments) | **Post** /v5/repos/{owner}/{repo}/pulls/{number}/comments    | 提交Pull Request评论                                    |
| *PullRequestsApi*  | [**PostV5ReposOwnerRepoPullsNumberLabels**](docs/PullRequestsApi.md#postv5reposownerrepopullsnumberlabels) | **Post** /v5/repos/{owner}/{repo}/pulls/{number}/labels      | 创建 Pull Request 标签                                  |
| *PullRequestsApi*  | [**PostV5ReposOwnerRepoPullsNumberTesters**](docs/PullRequestsApi.md#postv5reposownerrepopullsnumbertesters) | **Post** /v5/repos/{owner}/{repo}/pulls/{number}/testers     | 指派用户测试 Pull Request                               |
| *PullRequestsApi*  | [**PutV5ReposOwnerRepoPullsNumberLabels**](docs/PullRequestsApi.md#putv5reposownerrepopullsnumberlabels) | **Put** /v5/repos/{owner}/{repo}/pulls/{number}/labels       | 替换Pull Request 所有标签                               |
| *PullRequestsApi*  | [**PutV5ReposOwnerRepoPullsNumberMerge**](docs/PullRequestsApi.md#putv5reposownerrepopullsnumbermerge) | **Put** /v5/repos/{owner}/{repo}/pulls/{number}/merge        | 合并Pull Request                                        |
| *RepositoriesApi*  | [**DeleteV5ReposOwnerRepo**](docs/RepositoriesApi.md#deletev5reposownerrepo) | **Delete** /v5/repos/{owner}/{repo}                          | 删除一个仓库                                            |
| *RepositoriesApi*  | [**DeleteV5ReposOwnerRepoBranchesBranchProtection**](docs/RepositoriesApi.md#deletev5reposownerrepobranchesbranchprotection) | **Delete** /v5/repos/{owner}/{repo}/branches/{branch}/protection | 取消保护分支的设置                                      |
| *RepositoriesApi*  | [**DeleteV5ReposOwnerRepoCollaboratorsUsername**](docs/RepositoriesApi.md#deletev5reposownerrepocollaboratorsusername) | **Delete** /v5/repos/{owner}/{repo}/collaborators/{username} | 移除仓库成员                                            |
| *RepositoriesApi*  | [**DeleteV5ReposOwnerRepoCommentsId**](docs/RepositoriesApi.md#deletev5reposownerrepocommentsid) | **Delete** /v5/repos/{owner}/{repo}/comments/{id}            | 删除Commit评论                                          |
| *RepositoriesApi*  | [**DeleteV5ReposOwnerRepoContentsPath**](docs/RepositoriesApi.md#deletev5reposownerrepocontentspath) | **Delete** /v5/repos/{owner}/{repo}/contents/{path}          | 删除文件                                                |
| *RepositoriesApi*  | [**DeleteV5ReposOwnerRepoKeysEnableId**](docs/RepositoriesApi.md#deletev5reposownerrepokeysenableid) | **Delete** /v5/repos/{owner}/{repo}/keys/enable/{id}         | 停用仓库公钥                                            |
| *RepositoriesApi*  | [**DeleteV5ReposOwnerRepoKeysId**](docs/RepositoriesApi.md#deletev5reposownerrepokeysid) | **Delete** /v5/repos/{owner}/{repo}/keys/{id}                | 删除一个仓库公钥                                        |
| *RepositoriesApi*  | [**DeleteV5ReposOwnerRepoReleasesId**](docs/RepositoriesApi.md#deletev5reposownerreporeleasesid) | **Delete** /v5/repos/{owner}/{repo}/releases/{id}            | 删除仓库Release                                         |
| *RepositoriesApi*  | [**GetV5EnterprisesEnterpriseRepos**](docs/RepositoriesApi.md#getv5enterprisesenterpriserepos) | **Get** /v5/enterprises/{enterprise}/repos                   | 获取企业的所有仓库                                      |
| *RepositoriesApi*  | [**GetV5OrgsOrgRepos**](docs/RepositoriesApi.md#getv5orgsorgrepos) | **Get** /v5/orgs/{org}/repos                                 | 获取一个组织的仓库                                      |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepo**](docs/RepositoriesApi.md#getv5reposownerrepo) | **Get** /v5/repos/{owner}/{repo}                             | 获取用户的某个仓库                                      |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoBranches**](docs/RepositoriesApi.md#getv5reposownerrepobranches) | **Get** /v5/repos/{owner}/{repo}/branches                    | 获取所有分支                                            |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoBranchesBranch**](docs/RepositoriesApi.md#getv5reposownerrepobranchesbranch) | **Get** /v5/repos/{owner}/{repo}/branches/{branch}           | 获取单个分支                                            |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoCollaborators**](docs/RepositoriesApi.md#getv5reposownerrepocollaborators) | **Get** /v5/repos/{owner}/{repo}/collaborators               | 获取仓库的所有成员                                      |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoCollaboratorsUsername**](docs/RepositoriesApi.md#getv5reposownerrepocollaboratorsusername) | **Get** /v5/repos/{owner}/{repo}/collaborators/{username}    | 判断用户是否为仓库成员                                  |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoCollaboratorsUsernamePermission**](docs/RepositoriesApi.md#getv5reposownerrepocollaboratorsusernamepermission) | **Get** /v5/repos/{owner}/{repo}/collaborators/{username}/permission | 查看仓库成员的权限                                      |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoComments**](docs/RepositoriesApi.md#getv5reposownerrepocomments) | **Get** /v5/repos/{owner}/{repo}/comments                    | 获取仓库的Commit评论                                    |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoCommentsId**](docs/RepositoriesApi.md#getv5reposownerrepocommentsid) | **Get** /v5/repos/{owner}/{repo}/comments/{id}               | 获取仓库的某条Commit评论                                |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoCommits**](docs/RepositoriesApi.md#getv5reposownerrepocommits) | **Get** /v5/repos/{owner}/{repo}/commits                     | 仓库的所有提交                                          |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoCommitsRefComments**](docs/RepositoriesApi.md#getv5reposownerrepocommitsrefcomments) | **Get** /v5/repos/{owner}/{repo}/commits/{ref}/comments      | 获取单个Commit的评论                                    |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoCommitsSha**](docs/RepositoriesApi.md#getv5reposownerrepocommitssha) | **Get** /v5/repos/{owner}/{repo}/commits/{sha}               | 仓库的某个提交                                          |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoCompareBaseHead**](docs/RepositoriesApi.md#getv5reposownerrepocomparebasehead) | **Get** /v5/repos/{owner}/{repo}/compare/{base}...{head}     | 两个Commits之间对比的版本差异                           |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoContentsPath**](docs/RepositoriesApi.md#getv5reposownerrepocontentspath) | **Get** /v5/repos/{owner}/{repo}/contents/{path}             | 获取仓库具体路径下的内容                                |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoContributors**](docs/RepositoriesApi.md#getv5reposownerrepocontributors) | **Get** /v5/repos/{owner}/{repo}/contributors                | 获取仓库贡献者                                          |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoForks**](docs/RepositoriesApi.md#getv5reposownerrepoforks) | **Get** /v5/repos/{owner}/{repo}/forks                       | 查看仓库的Forks                                         |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoKeys**](docs/RepositoriesApi.md#getv5reposownerrepokeys) | **Get** /v5/repos/{owner}/{repo}/keys                        | 获取仓库已部署的公钥                                    |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoKeysAvailable**](docs/RepositoriesApi.md#getv5reposownerrepokeysavailable) | **Get** /v5/repos/{owner}/{repo}/keys/available              | 获取仓库可部署的公钥                                    |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoKeysId**](docs/RepositoriesApi.md#getv5reposownerrepokeysid) | **Get** /v5/repos/{owner}/{repo}/keys/{id}                   | 获取仓库的单个公钥                                      |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoPages**](docs/RepositoriesApi.md#getv5reposownerrepopages) | **Get** /v5/repos/{owner}/{repo}/pages                       | 获取Pages信息                                           |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoReadme**](docs/RepositoriesApi.md#getv5reposownerreporeadme) | **Get** /v5/repos/{owner}/{repo}/readme                      | 获取仓库README                                          |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoReleases**](docs/RepositoriesApi.md#getv5reposownerreporeleases) | **Get** /v5/repos/{owner}/{repo}/releases                    | 获取仓库的所有Releases                                  |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoReleasesId**](docs/RepositoriesApi.md#getv5reposownerreporeleasesid) | **Get** /v5/repos/{owner}/{repo}/releases/{id}               | 获取仓库的单个Releases                                  |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoReleasesLatest**](docs/RepositoriesApi.md#getv5reposownerreporeleaseslatest) | **Get** /v5/repos/{owner}/{repo}/releases/latest             | 获取仓库的最后更新的Release                             |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoReleasesTagsTag**](docs/RepositoriesApi.md#getv5reposownerreporeleasestagstag) | **Get** /v5/repos/{owner}/{repo}/releases/tags/{tag}         | 根据Tag名称获取仓库的Release                            |
| *RepositoriesApi*  | [**GetV5ReposOwnerRepoTags**](docs/RepositoriesApi.md#getv5reposownerrepotags) | **Get** /v5/repos/{owner}/{repo}/tags                        | 列出仓库所有的tags                                      |
| *RepositoriesApi*  | [**GetV5UserRepos**](docs/RepositoriesApi.md#getv5userrepos) | **Get** /v5/user/repos                                       | 列出授权用户的所有仓库                                  |
| *RepositoriesApi*  | [**GetV5UsersUsernameRepos**](docs/RepositoriesApi.md#getv5usersusernamerepos) | **Get** /v5/users/{username}/repos                           | 获取某个用户的公开仓库                                  |
| *RepositoriesApi*  | [**PatchV5ReposOwnerRepo**](docs/RepositoriesApi.md#patchv5reposownerrepo) | **Patch** /v5/repos/{owner}/{repo}                           | 更新仓库设置                                            |
| *RepositoriesApi*  | [**PatchV5ReposOwnerRepoCommentsId**](docs/RepositoriesApi.md#patchv5reposownerrepocommentsid) | **Patch** /v5/repos/{owner}/{repo}/comments/{id}             | 更新Commit评论                                          |
| *RepositoriesApi*  | [**PatchV5ReposOwnerRepoReleasesId**](docs/RepositoriesApi.md#patchv5reposownerreporeleasesid) | **Patch** /v5/repos/{owner}/{repo}/releases/{id}             | 更新仓库Release                                         |
| *RepositoriesApi*  | [**PostV5EnterprisesEnterpriseRepos**](docs/RepositoriesApi.md#postv5enterprisesenterpriserepos) | **Post** /v5/enterprises/{enterprise}/repos                  | 创建企业仓库                                            |
| *RepositoriesApi*  | [**PostV5OrgsOrgRepos**](docs/RepositoriesApi.md#postv5orgsorgrepos) | **Post** /v5/orgs/{org}/repos                                | 创建组织仓库                                            |
| *RepositoriesApi*  | [**PostV5ReposOwnerRepoBranches**](docs/RepositoriesApi.md#postv5reposownerrepobranches) | **Post** /v5/repos/{owner}/{repo}/branches                   | 创建分支                                                |
| *RepositoriesApi*  | [**PostV5ReposOwnerRepoCommitsShaComments**](docs/RepositoriesApi.md#postv5reposownerrepocommitsshacomments) | **Post** /v5/repos/{owner}/{repo}/commits/{sha}/comments     | 创建Commit评论                                          |
| *RepositoriesApi*  | [**PostV5ReposOwnerRepoContentsPath**](docs/RepositoriesApi.md#postv5reposownerrepocontentspath) | **Post** /v5/repos/{owner}/{repo}/contents/{path}            | 新建文件                                                |
| *RepositoriesApi*  | [**PostV5ReposOwnerRepoForks**](docs/RepositoriesApi.md#postv5reposownerrepoforks) | **Post** /v5/repos/{owner}/{repo}/forks                      | Fork一个仓库                                            |
| *RepositoriesApi*  | [**PostV5ReposOwnerRepoKeys**](docs/RepositoriesApi.md#postv5reposownerrepokeys) | **Post** /v5/repos/{owner}/{repo}/keys                       | 为仓库添加公钥                                          |
| *RepositoriesApi*  | [**PostV5ReposOwnerRepoPagesBuilds**](docs/RepositoriesApi.md#postv5reposownerrepopagesbuilds) | **Post** /v5/repos/{owner}/{repo}/pages/builds               | 请求建立Pages                                           |
| *RepositoriesApi*  | [**PostV5ReposOwnerRepoReleases**](docs/RepositoriesApi.md#postv5reposownerreporeleases) | **Post** /v5/repos/{owner}/{repo}/releases                   | 创建仓库Release                                         |
| *RepositoriesApi*  | [**PostV5UserRepos**](docs/RepositoriesApi.md#postv5userrepos) | **Post** /v5/user/repos                                      | 创建一个仓库                                            |
| *RepositoriesApi*  | [**PutV5ReposOwnerRepoBranchesBranchProtection**](docs/RepositoriesApi.md#putv5reposownerrepobranchesbranchprotection) | **Put** /v5/repos/{owner}/{repo}/branches/{branch}/protection | 设置分支保护                                            |
| *RepositoriesApi*  | [**PutV5ReposOwnerRepoClear**](docs/RepositoriesApi.md#putv5reposownerrepoclear) | **Put** /v5/repos/{owner}/{repo}/clear                       | 清空一个仓库                                            |
| *RepositoriesApi*  | [**PutV5ReposOwnerRepoCollaboratorsUsername**](docs/RepositoriesApi.md#putv5reposownerrepocollaboratorsusername) | **Put** /v5/repos/{owner}/{repo}/collaborators/{username}    | 添加仓库成员                                            |
| *RepositoriesApi*  | [**PutV5ReposOwnerRepoContentsPath**](docs/RepositoriesApi.md#putv5reposownerrepocontentspath) | **Put** /v5/repos/{owner}/{repo}/contents/{path}             | 更新文件                                                |
| *RepositoriesApi*  | [**PutV5ReposOwnerRepoKeysEnableId**](docs/RepositoriesApi.md#putv5reposownerrepokeysenableid) | **Put** /v5/repos/{owner}/{repo}/keys/enable/{id}            | 启用仓库公钥                                            |
| *RepositoriesApi*  | [**PutV5ReposOwnerRepoReviewer**](docs/RepositoriesApi.md#putv5reposownerreporeviewer) | **Put** /v5/repos/{owner}/{repo}/reviewer                    | 修改代码审查设置                                        |
| *SearchApi*        | [**GetV5SearchGists**](docs/SearchApi.md#getv5searchgists)   | **Get** /v5/search/gists                                     | 搜索代码片段                                            |
| *SearchApi*        | [**GetV5SearchIssues**](docs/SearchApi.md#getv5searchissues) | **Get** /v5/search/issues                                    | 搜索 Issues                                             |
| *SearchApi*        | [**GetV5SearchRepositories**](docs/SearchApi.md#getv5searchrepositories) | **Get** /v5/search/repositories                              | 搜索仓库                                                |
| *SearchApi*        | [**GetV5SearchUsers**](docs/SearchApi.md#getv5searchusers)   | **Get** /v5/search/users                                     | 搜索用户                                                |
| *UsersApi*         | [**DeleteV5UserFollowingUsername**](docs/UsersApi.md#deletev5userfollowingusername) | **Delete** /v5/user/following/{username}                     | 取消关注一个用户                                        |
| *UsersApi*         | [**DeleteV5UserKeysId**](docs/UsersApi.md#deletev5userkeysid) | **Delete** /v5/user/keys/{id}                                | 删除一个公钥                                            |
| *UsersApi*         | [**GetV5User**](docs/UsersApi.md#getv5user)                  | **Get** /v5/user                                             | 获取授权用户的资料                                      |
| *UsersApi*         | [**GetV5UserFollowers**](docs/UsersApi.md#getv5userfollowers) | **Get** /v5/user/followers                                   | 列出授权用户的关注者                                    |
| *UsersApi*         | [**GetV5UserFollowing**](docs/UsersApi.md#getv5userfollowing) | **Get** /v5/user/following                                   | 列出授权用户正关注的用户                                |
| *UsersApi*         | [**GetV5UserFollowingUsername**](docs/UsersApi.md#getv5userfollowingusername) | **Get** /v5/user/following/{username}                        | 检查授权用户是否关注了一个用户                          |
| *UsersApi*         | [**GetV5UserKeys**](docs/UsersApi.md#getv5userkeys)          | **Get** /v5/user/keys                                        | 列出授权用户的所有公钥                                  |
| *UsersApi*         | [**GetV5UserKeysId**](docs/UsersApi.md#getv5userkeysid)      | **Get** /v5/user/keys/{id}                                   | 获取一个公钥                                            |
| *UsersApi*         | [**GetV5UserNamespace**](docs/UsersApi.md#getv5usernamespace) | **Get** /v5/user/namespace                                   | 获取授权用户的一个 Namespace                            |
| *UsersApi*         | [**GetV5UserNamespaces**](docs/UsersApi.md#getv5usernamespaces) | **Get** /v5/user/namespaces                                  | 列出授权用户所有的 Namespace                            |
| *UsersApi*         | [**GetV5UsersUsername**](docs/UsersApi.md#getv5usersusername) | **Get** /v5/users/{username}                                 | 获取一个用户                                            |
| *UsersApi*         | [**GetV5UsersUsernameFollowers**](docs/UsersApi.md#getv5usersusernamefollowers) | **Get** /v5/users/{username}/followers                       | 列出指定用户的关注者                                    |
| *UsersApi*         | [**GetV5UsersUsernameFollowing**](docs/UsersApi.md#getv5usersusernamefollowing) | **Get** /v5/users/{username}/following                       | 列出指定用户正在关注的用户                              |
| *UsersApi*         | [**GetV5UsersUsernameFollowingTargetUser**](docs/UsersApi.md#getv5usersusernamefollowingtargetuser) | **Get** /v5/users/{username}/following/{target_user}         | 检查指定用户是否关注目标用户                            |
| *UsersApi*         | [**GetV5UsersUsernameKeys**](docs/UsersApi.md#getv5usersusernamekeys) | **Get** /v5/users/{username}/keys                            | 列出指定用户的所有公钥                                  |
| *UsersApi*         | [**PatchV5User**](docs/UsersApi.md#patchv5user)              | **Patch** /v5/user                                           | 更新授权用户的资料                                      |
| *UsersApi*         | [**PostV5UserKeys**](docs/UsersApi.md#postv5userkeys)        | **Post** /v5/user/keys                                       | 添加一个公钥                                            |
| *UsersApi*         | [**PutV5UserFollowingUsername**](docs/UsersApi.md#putv5userfollowingusername) | **Put** /v5/user/following/{username}                        | 关注一个用户                                            |
| *WebhooksApi*      | [**DeleteV5ReposOwnerRepoHooksId**](docs/WebhooksApi.md#deletev5reposownerrepohooksid) | **Delete** /v5/repos/{owner}/{repo}/hooks/{id}               | 删除一个仓库WebHook                                     |
| *WebhooksApi*      | [**GetV5ReposOwnerRepoHooks**](docs/WebhooksApi.md#getv5reposownerrepohooks) | **Get** /v5/repos/{owner}/{repo}/hooks                       | 列出仓库的WebHooks                                      |
| *WebhooksApi*      | [**GetV5ReposOwnerRepoHooksId**](docs/WebhooksApi.md#getv5reposownerrepohooksid) | **Get** /v5/repos/{owner}/{repo}/hooks/{id}                  | 获取仓库单个WebHook                                     |
| *WebhooksApi*      | [**PatchV5ReposOwnerRepoHooksId**](docs/WebhooksApi.md#patchv5reposownerrepohooksid) | **Patch** /v5/repos/{owner}/{repo}/hooks/{id}                | 更新一个仓库WebHook                                     |
| *WebhooksApi*      | [**PostV5ReposOwnerRepoHooks**](docs/WebhooksApi.md#postv5reposownerrepohooks) | **Post** /v5/repos/{owner}/{repo}/hooks                      | 创建一个仓库WebHook                                     |
| *WebhooksApi*      | [**PostV5ReposOwnerRepoHooksIdTests**](docs/WebhooksApi.md#postv5reposownerrepohooksidtests) | **Post** /v5/repos/{owner}/{repo}/hooks/{id}/tests           | 测试WebHook是否发送成功                                 |


## 文档模式

 - [BasicInfo](docs/BasicInfo.md)
 - [Blob](docs/Blob.md)
 - [Branch](docs/Branch.md)
 - [BranchCommit](docs/BranchCommit.md)
 - [BranchProtectionPutParam](docs/BranchProtectionPutParam.md)
 - [Code](docs/Code.md)
 - [CodeComment](docs/CodeComment.md)
 - [CodeForks](docs/CodeForks.md)
 - [CodeForksHistory](docs/CodeForksHistory.md)
 - [Commit](docs/Commit.md)
 - [CommitContent](docs/CommitContent.md)
 - [CommitTree](docs/CommitTree.md)
 - [Compare](docs/Compare.md)
 - [CompleteBranch](docs/CompleteBranch.md)
 - [Content](docs/Content.md)
 - [ContentBasic](docs/ContentBasic.md)
 - [Contributor](docs/Contributor.md)
 - [CreateBranchParam](docs/CreateBranchParam.md)
 - [CreatePullRequestParam](docs/CreatePullRequestParam.md)
 - [Email](docs/Email.md)
 - [EnterpriseBasic](docs/EnterpriseBasic.md)
 - [EnterpriseMember](docs/EnterpriseMember.md)
 - [Event](docs/Event.md)
 - [GitCommit](docs/GitCommit.md)
 - [GitUser](docs/GitUser.md)
 - [Group](docs/Group.md)
 - [GroupDetail](docs/GroupDetail.md)
 - [GroupMember](docs/GroupMember.md)
 - [Hook](docs/Hook.md)
 - [Issue](docs/Issue.md)
 - [IssueCommentPostParam](docs/IssueCommentPostParam.md)
 - [IssueUpdateParam](docs/IssueUpdateParam.md)
 - [Label](docs/Label.md)
 - [LabelPostParam](docs/LabelPostParam.md)
 - [Milestone](docs/Milestone.md)
 - [Namespace](docs/Namespace.md)
 - [NamespaceMini](docs/NamespaceMini.md)
 - [NewFileParam](docs/NewFileParam.md)
 - [Note](docs/Note.md)
 - [OperateLog](docs/OperateLog.md)
 - [ProgramBasic](docs/ProgramBasic.md)
 - [Project](docs/Project.md)
 - [ProjectBasic](docs/ProjectBasic.md)
 - [ProjectMember](docs/ProjectMember.md)
 - [ProjectMemberPermission](docs/ProjectMemberPermission.md)
 - [ProjectMemberPutParam](docs/ProjectMemberPutParam.md)
 - [PullRequest](docs/PullRequest.md)
 - [PullRequestAssigneePostParam](docs/PullRequestAssigneePostParam.md)
 - [PullRequestCommentPatchParam](docs/PullRequestCommentPatchParam.md)
 - [PullRequestCommentPostParam](docs/PullRequestCommentPostParam.md)
 - [PullRequestComments](docs/PullRequestComments.md)
 - [PullRequestCommits](docs/PullRequestCommits.md)
 - [PullRequestFilePath](docs/PullRequestFilePath.md)
 - [PullRequestFiles](docs/PullRequestFiles.md)
 - [PullRequestLabelPostParam](docs/PullRequestLabelPostParam.md)
 - [PullRequestMergePutParam](docs/PullRequestMergePutParam.md)
 - [PullRequestUpdateParam](docs/PullRequestUpdateParam.md)
 - [Release](docs/Release.md)
 - [RepoCommit](docs/RepoCommit.md)
 - [RepoPatchParam](docs/RepoPatchParam.md)
 - [RepositoryPostParam](docs/RepositoryPostParam.md)
 - [SetRepoReviewer](docs/SetRepoReviewer.md)
 - [SingleCommit](docs/SingleCommit.md)
 - [SshKey](docs/SshKey.md)
 - [SshKeyBasic](docs/SshKeyBasic.md)
 - [Tag](docs/Tag.md)
 - [Tree](docs/Tree.md)
 - [TreeBasic](docs/TreeBasic.md)
 - [User](docs/User.md)
 - [UserBasic](docs/UserBasic.md)
 - [UserMessage](docs/UserMessage.md)
 - [UserMessageList](docs/UserMessageList.md)
 - [UserMini](docs/UserMini.md)
 - [UserNotification](docs/UserNotification.md)
 - [UserNotificationCount](docs/UserNotificationCount.md)
 - [UserNotificationList](docs/UserNotificationList.md)
 - [UserNotificationNamespace](docs/UserNotificationNamespace.md)
 - [UserNotificationSubject](docs/UserNotificationSubject.md)
 - [WeekReport](docs/WeekReport.md)

## 软件许可

详情请见 [LICENSE](LICENSE)文件 。

