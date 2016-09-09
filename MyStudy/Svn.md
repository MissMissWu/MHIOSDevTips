# SVN
---

## 开篇扯淡

trunk：表示开发时版本存放的目录，即在开发阶段的代码都提交到该目录上。

branches：表示发布的版本存放的目录，即项目上线时发布的稳定版本存放在该目录中。

tags：表示标签存放的目录。

* SVN常用命令


  ```0bjc
  svn import  : 将文件导入到服务器
  svn checkout: 下载服务器的代码到本地   (简写svn co)
  svn commit  : 将改动的文件提交到服务器  (简写svn ci)
  svn update  : 更新服务器的代码到本地   (简写svn up)
  svn add     : 向本地的版本控制库中添加新文件
  svn delete  : 从本地的版本控制库中删除文件 (简写svn del)
  svn remove  : 从本地的版本控制库中删除文件(简写svn rm)
  svn move    : 移动文件或者目录或文件更名
  svn mkdir   : 创建纳入版本控制下的新目录
  svn revert  : 撤销之前的一切修改
  svn merge   : 将两个版本之间的差异合并到当前文件
  svn info    : 查看文件的详细信息
  svn diff    : 查看不同版本的区别
  svn log     : 查看日志信息
  svn list    : 列出版本库下的文件和目录列表
  svn status  : 查看文件状态（简写svn st）
  svn help    : 获取帮助信息（比如svn help ci）
  svn lock    : 加锁
  svn unlock  : 解锁
  更多命令，使用svn help 进行查看
  svn help [命令] // 可以查看命令帮助
  ```



* SVN文件状态标识

  ```objc
  使用文件状态命令 svn st 查看文件状态时的标识
  ' ' 没有修改
  'A' 被添加到本地代码仓库
  'C' 冲突
  'D' 被删除
  'I' 被忽略
  'M' 被修改
  'R' 被替换
  'X' 外部定义创建的版本目录
  '?' 文件没有被添加到本地版本库内
  '!' 文件丢失或者不完整（不是通过svn命令删除的文件）
  '~' 受控文件被其他文件阻隔
  ```

## 参考链接
* Versions
  - <http://blog.csdn.net/u013368288/article/details/23885975>
  - <http://blog.csdn.net/jeffasd/article/details/50510678>

* SVN 主干(trunk)、分支(branch )、标记(tag)
  - <http://panfuy.iteye.com/blog/1278865>
  - <http://www.thegeekstuff.com/2014/03/svn-merge-command/>


* SVN的合并与分支
  - <http://www.cnblogs.com/mq0036/p/3498908.html>
  - <http://www.panweizeng.com/svn-branching-merging.html>
  - 


* SVN命令
  - <http://www.tuicool.com/articles/M7FJbiq>
  - <http://blog.sina.com.cn/s/blog_74e9d98d01017pmn.html>
  - <http://www.cnblogs.com/luckythan/p/4478706.html>
  - <http://www.cnblogs.com/heiniuhaha/archive/2011/11/11/2245594.html>
  - <http://www.cnblogs.com/snandy/p/4072857.html>
  - <http://blog.csdn.net/wswqiang/article/details/7954061>
  - <http://www.2cto.com/os/201206/134647.html>
  - <http://www.cnblogs.com/wangrui-techbolg/archive/2013/08/20/3270058.html>
  - <http://blog.sina.com.cn/s/blog_5fb39f910101be7i.html>
  - <http://www.2cto.com/os/201305/210296.html>
  - <http://blog.csdn.net/binsoft/article/details/44624577>
  - <http://www.thegeekstuff.com/2011/04/svn-command-examples/>
  - <http://www.jianshu.com/p/d46b92d4facc>
  - 

* svn 命令行创建和删除 分支和tags
  - <http://blog.csdn.net/yangzhongxuan/article/details/7519948>
  - <http://www.panweizeng.com/svn-branching-merging.html>


* 如何在MAC环境下(Xcode)使用svn，以及新手在团队使用svn注意事项
  - <http://blog.csdn.net/mad1989/article/details/12975815>


* SVN错误
  - ` 
  svn: E155036: Please see the 'svn upgrade' command
svn: E155036: Working copy '/home/easwy/dev' is too old (format 10, created by Subversion 1.6)
`
    - <http://blog.sina.com.cn/s/blog_7c8dc2d50101mwm1.html>
    - <http://easwy.com/blog/archives/svn-upgrade-and-switch/>
    - <http://www.jianshu.com/p/40f95ad8fa64>
    - <http://blog.csdn.net/centralperk/article/details/48736031> 

  - ` SVN：This client is too old to work with working copy…解决办法`
    - <http://blog.csdn.net/wu407797466/article/details/7946269>
    - <http://qa.blog.163.com/blog/static/190147002201161263424860/>
    - <http://blog.csdn.net/kazeik/article/details/41443545>


* SVN详解
  - <http://www.jianshu.com/p/641438b9ab43>
  - <http://www.jianshu.com/p/94498251c7c8>


* Cornerstone
  - 使用教程
    - <http://blog.csdn.net/gf771115/article/details/41008853>
    - <http://www.jianshu.com/p/7f5c019c528b> 
    - <http://blog.csdn.net/kerry_deng/article/details/46287389>
    - 
  - Cornerstone设置的忽略文件
    - <http://www.jianshu.com/p/d662ca680c3d>
    - <http://www.cnblogs.com/Apologize/p/5019900.html>
    - <>
  - Cornerstone合并分支
    - <http://blog.csdn.net/leleyuan1130/article/details/50628450>
    - <http://www.jianshu.com/p/d97b1d82d6cf>
    - <http://blog.csdn.net/lijuan3203/article/details/52121353>
    - <>

* iOS开发——开发实战篇&版本控制SVN和Git使用详解
  - <http://www.cnblogs.com/iCocos/p/4767692.html>
  - 