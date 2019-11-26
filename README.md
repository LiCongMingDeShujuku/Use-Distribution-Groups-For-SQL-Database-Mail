![CLEVER DATA GIT REPO](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/0-clever-data-github.png "李聪明的数据库")

# 使用数据库邮件的通讯组
#### Use Distribution Groups For SQL Database Mail
**发布-日期: 2015年06月29日 (评论)**


## Contents

- [中文](#中文)
- [English](#English)
- [SQL Logic](#Logic)
- [Build Info](#Build-Info)
- [Author](#Author)
- [License](#License) 


## 中文
你将在线找到许多关于如何配置SQL数据库邮件的示例。这些工作非常适合演示这个过程，但有些人可能会对“收件人”实际使用的内容感到困惑。简单地使用通讯组其实是更好的选择。如果你需要向电子邮件通知中添加更多人，只需将其添加到通讯组即可。除此以外，你最终会在工作中的通知步骤中编码电子邮件地址。这样做完全没有效率。是否有多种“类型”警报发生了？创建更多通讯组并相应地应用它们。请不要直接在通知逻辑中解决问题。

示例通知逻辑：

## English

You’ll find many examples online on how to configure SQL Database Mail. These work great to demonstrate the process, but some might get confused on what to actually use for the ‘recipients’. It’s better to simply use a distribution group. If you need to add more people to the email notifications simply add them to the distribution group. Otherwise; you would end up hardcoding email addresses in and out of your notification steps within your jobs. Not a good idea, and completely inefficient. Have more than one ‘type’ of alerts going on? Create more distribution groups and apply them accordingly. Do not mettle around directly in your notification logic if you can help it.

Sample notification logic:
---
## Logic
```SQL
declare @server_name varchar(255)
declare @job_name varchar(255)
declare @message_subject varchar(255)
declare @message_body varchar(max)
 
set @server_name = (select @@servername )
set @job_name = (select name from msdb.dbo.sysjobs where @jobid = convert(uniqueidentifier, $(escape_none(jobid))))
set @message_subject = (select 'Job Failure on Server: ' + @server_name + ' Job: ' + @job_name
set @message_body = @message_subject + char(10) + char(10) + 'The Job failed at step (step name):'
 
EXEC msdb.dbo.sp_send_dbmail
@profile_name = 'SQLDatabaseMailProfile'
, &lt;em&gt;@recipients = 'AnotherEmailAddress@mydomain.com', 'AnotherEmailAddress', 'AnotherEmailAddress'&lt;/em&gt; &lt;img src="https://mikesdatawork.files.wordpress.com/2015/06/image002.png" alt="" width="14" height="14" class="alignnone size-full wp-image-568" /&gt; NOT efficient.
, @recipients = 'sqladminalerts@mydomain.com' &lt;img src="https://mikesdatawork.files.wordpress.com/2015/06/image002.png" alt="" width="14" height="14" class="alignnone size-full wp-image-568" /&gt; More efficient. Use distribution groups.
, @subject = @message_subject
, @body = @message_body


```
![#](images/use-distribution-lists-groups-for-sql-notifications.png?raw=true "#")



[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

- **李聪明的数据库 Lee's Clever Data**
- **Mike的数据库宝典 Mikes Database Collection**
- **李聪明的数据库** "Lee Songming"

[![Gist](https://img.shields.io/badge/Gist-李聪明的数据库-<COLOR>.svg)](https://gist.github.com/congmingshuju)
[![Twitter](https://img.shields.io/badge/Twitter-mike的数据库宝典-<COLOR>.svg)](https://twitter.com/mikesdatawork?lang=en)
[![Wordpress](https://img.shields.io/badge/Wordpress-mike的数据库宝典-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)

---
## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Lee Songming](https://raw.githubusercontent.com/LiCongMingDeShujuku/git-resources/master/1-clever-data-github.png "李聪明的数据库")

