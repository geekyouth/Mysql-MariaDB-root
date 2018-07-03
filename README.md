# Mysql-MariaDB-root

Win 版本MariaDB 、Mysql 数据库误删 root 用户无法登录的无损补救措施


----------
今天在使用MariaDB 时，手贱把权限管理用户列表下的全部用户删光了。

![][1]
上图为危险动作，请勿模拟。

然后就悲剧了，没有账户无法登陆。难道要重装吗？太麻烦了，而且数据极有可能丢失，大概搜了一下google ，找到了灵感。开始之前先介绍下开发环境：本人使用Win10 笔记本，数据库软件Mariadb 10.2，数据库管理软件是Mariadb 自带的Heidisql，超级好用。

至于MariaDB，这是Mysql的一个分支，和Mysql 无缝兼容，开源免费，至于他和 Mysql 之间的爱恨情仇可以写一本书了，这里简而言之，反正你只要知道这个MariaDB 其实就是原汁原味的 Mysql 就OK。而且个人推荐你长期使用这个版本，因为原本开源免费的Mysql 已经被商业公司Oracle 收购了，后面的故事我想你大概知道结果。

以下是恢复数据库 root 账户的具体步骤，Mysql 版本可以参考此方法。

1-进入Mariadb安装目录，data下面的my.ini配置文件：

添加跳过权限检测代码：

> skip-grant-tables

然后保存文件【如果无法操作此文件，你可能需要先关闭Mysql 服务，见下文】。

![][2]

2-快捷键 ctrl+shift+esc 进入任务管理器，找到进程---后台进程---Mysqld.exe，下箭头Mysql，右键打开服务：

![][3]
3-这时Mysql 应该是启动状态，手动停止Mysql 服务再打开服务，也就是重启：

![][4]

4-打开Mysql 管理软件HeidiSQL ，localhost 随意输入账户 即可登入，然后点击用户管理图标添加root 用户如下图：

![][5]

5-添加成功后，删掉my.ini 配置文件里的高危代码，恢复之前的样子：

![][6]

6-再次重启Mysql 服务，之后即可正常使用MariaDB。。。

![][7]

本文首发于极客青年博客：[https://52geek.top/106/][9]，转载请注明出处，谢谢。


  [1]: http://p7fcrq2e4.bkt.clouddn.com/201818031910-heidisql20180703_191013.png
  [2]: http://p7fcrq2e4.bkt.clouddn.com/201818031912-sublime_text20180703_191250.png
  [3]: http://p7fcrq2e4.bkt.clouddn.com/201818031916-Taskmgr20180703_191612.png
  [4]: http://p7fcrq2e4.bkt.clouddn.com/201818031920-20180703_192018.png
  [5]: http://p7fcrq2e4.bkt.clouddn.com/201818031922-heidisql20180703_192237.png
  [6]: http://p7fcrq2e4.bkt.clouddn.com/201818031924-sublime_text20180703_192429.png
  [7]: http://p7fcrq2e4.bkt.clouddn.com/201818031920-20180703_192018.png
  [9]: https://52geek.top/106/
