# CocoaPods

### Pod Trunk \(发布自己的源码到 CocoaPods\)

### 利用pod trunk发布程序

---

##### 注册

* `pod trunk register  邮箱 '用户名' --description='电脑描述'`

##### 查收邮件

* 如果是QQ邮箱，可能会被放到“垃圾箱”中，并不一定是“收件箱”
* 点击邮件中的链接：
  [https:\/\/trunk.cocoapods.org\/sessions\/verify\/xxxx](https://trunk.cocoapods.org/sessions/verify/xxxx)

##### 接下来查看个人信息

* `pod trunk me`

```
  - Name:     MJ Lee
  - Email:    xxxxxx@qq.com
  - Since:    January 28th, 03:53
  - Pods:     None
  - Sessions:
    - January 28th, 04:28 - June 5th, 04:34. IP: xxx.xxx.xxx.xxx Description: Macbook Pro
```

* 中间可能遇到这种错误

```
NoMethodError - undefined method 'last' for #<Netrc::Entry:0x007fc59c246378>
```

* 这时候需要尝试更新gem源或者pod
  * `sudo gem update --system`
  * `sudo gem install cocoapods`  
  * `sudo gem install cocospods-trunk`  


##### 创建podspec文件

* 接下来需要在项目根路径创建一个podspec文件来描述你的项目信息  
  * `pod spec create 文件名`  
  * 比如pod spec create MJExtension就会生成一个MJExtension.podspec


##### 填写podspec内容

```
Pod::Spec.new do |s|
  s.name         = "MJExtension"
  s.version      = "0.0.1"
  s.summary      = "The fastest and most convenient conversion between JSON and model"
  s.homepage     = "https://github.com/CoderMJLee/MJExtension"
  s.license      = "MIT"
  s.author             = { "MJLee" => "xxxxx@qq.com" }
  s.social_media_url   = "http://weibo.com/exceptions"
  s.source       = { :git => "https://github.com/CoderMJLee/MJExtension.git", :tag => s.version }
  s.source_files  = "MJExtensionExample/MJExtensionExample/MJExtension"
  s.requires_arc = true
end
```

* 值得注意的是，现在的podspec必须有tag，所以最好先打个tag，传到github  
  * `git tag 0.0.1`    
  * `git push --tags`


##### 检测podspec语法

* `pod spec lint MJExtension.podspec`

##### 发布podspec

* `pod trunk push MJExtension.podspec`  
* 如果是第一次发布pod，需要去 [https:\/\/trunk.cocoapods.org\/claims\/new](https://trunk.cocoapods.org/claims/new)  认领pod

##### 检测

* `pod setup` : 初始化
* `pod repo update` : 更新仓库
* `pod search MJExtension`

##### 仓库更新

* 如果仓库更新慢，可以考虑更换仓库镜像
  * `pod repo remove master`
  * `pod repo add master http://git.oschina.net/akuandev/Specs.git`


##### pod trunk 细节

* podspec 参数解释

  * name ：pod的名字，应该与你的工程名保持一致 
  * version： 版本号，你以为是你工程的版本号，那你就大错特错了，我在这个地方坑了好久。后来才知道这个version是和你的branch名称保持一致的，如果你的branch名字叫做1.0.0，那这个version就可以要写成1.0.0，当更新版本的时候，要重新建立一个branch命名为1.0.1，然后version也要写成1.0.1。
  * summary：一句话介绍你的pod 
  * homepage：pod的url地址 
  * license：你的pod所遵守的开源协议、 一般都是‘MIT’ 
  * author： 作者名，联系方式 
  * platform：pod所支持平台和最小系统版本

  * source：pod的地址和tag

  * source\_files：pod在工程中的所在目录，如果有多个不同的目录，则写成这种形式:’floder1…’,’floder2….’,’….’ 
  * requires\_arc：是否是ARC。  
    **注意**: source\_files中指定的.h .m文件一定不要引用source\_files以外文件中的变量，头文件等，不然后面会出错,会说的source\_files路径下 `xxxx.h not found` 。source\_files中的文件应该是独立的模块。


##### 参考链接

* [http:\/\/www.bkjia.com\/Androidjc\/1005147.html](http://www.bkjia.com/Androidjc/1005147.html)
* [http:\/\/www.cnblogs.com\/wengzilin\/p\/4742530.html](http://www.cnblogs.com/wengzilin/p/4742530.html)
* [http:\/\/www.cocoachina.com\/ios\/20150228\/11206.html](http://www.cocoachina.com/ios/20150228/11206.html)
* [http:\/\/www.jianshu.com\/p\/1139a603f413](http://www.jianshu.com/p/1139a603f413)

### 拓展

---

* `pod spec lint`：老是报之前的错误，但你已经解决，很可能是CococPods缓存引起的。解决办法：终端上执行 `sudo rm -fr ~/Library/Caches/CocoaPods/` 然后重新 `pod spec lint`
* 删除本地tag和远程tag 删除本地 `git tag -d <tagname>`  删除远程 `git push origin :refs/tags/<tagname>` **注意**：删除分支后  最好清理一下 cocoapods的缓存   
   **参考链接** ：[http:\/\/blog.csdn.net\/majiakun1\/article\/details\/50730457](http://blog.csdn.net/majiakun1/article/details/50730457)
* pod search细节 ：pod search只会搜索你本地缓存的框架，如果你想搜索到最新的第三方框架或者某个框架的最新版本，必须先使用pod repo update（推荐）或者pod setup将远程仓库的框架信息更新到本地。其实，从pod search的响应速度飞快，也可以猜出它并没有连接服务器，仅仅是搜索了本地的框架信息\[呵呵\]
    此外，如果你的框架更新比较慢，可以尝试执行下面2条指令更换镜像服务器

  ```
    pod repo remove master
    pod repo add master http://git.oschina.net/akuandev/Specs.git
  ```

  更换镜像完毕后，以后执行pod repo update的速度就会快很多


## Cocoapods

---

* [cocoapods的使用](http://www.cnblogs.com/wayne23/p/3912882.html)

* [cocapods的使用以及常用问题](http://www.jianshu.com/p/6e5c0f78200a)
* 



