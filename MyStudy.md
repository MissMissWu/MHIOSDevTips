# MyStudy
---

## 开篇扯淡
好的资料的收集。

## 收集资料

```objc
（1）__FUNCTION__   ： // 获取当前方法名；
（2）__func__   ： // 获取当前方法名；
（3）__PRETTY_FUNCTION__   ： // 获取当前方法名；
（4）__LINE__   ： // 获取当前所在行；
（5）__FILE__   ： // 获取该文件的绝对路径；
（6）__DATE__   ： // 获取当前日期；
（7）__TIME__   ： // 获取当前时分秒；
（8）__TIMESTAMP__   ： // 获取当前时间戳；
```
```
presentedViewController和presentingViewController，他们分别是被present的控制器和正在presenting的控制器。   
比如说: 
控制器A和B，[A presentViewController B animated：YES completion：nil]; 那么A相对于B就是presentingViewController，B相对于A是presentedViewController.  
即这个时候　　
　　　　B.presentingViewController = A;
　　　　A.presentedViewController = B;
```

## 参考链接
* [layoutSubviews总结](http://blog.csdn.net/doubleuto/article/details/45155677)

* [ios时间那点事--NSCalendar NSDateComponents](http://my.oschina.net/yongbin45/blog/156181)

* [iOS10个实用小技巧（总有你不知道的和你会用到的）](http://www.jianshu.com/p/a3156826c27c)

* [Xcode因为证书问题经常报的那些](http://www.jianshu.com/p/b10680a32d35)

* [iOS之下拉放大，上推缩小，一个方法搞定](http://www.jianshu.com/p/eae68e8e0838)

* [各种图标图Demo](http://echarts.baidu.com/examples.html)

* [iOS 开发中你是否遇到这些经验问题(一)](http://www.jianshu.com/p/8207621ddcaa)

* [iOS开发几年了，你清楚OC中的这些东西么!!!](http://www.jianshu.com/p/bd496d5ef150)

* [21个优质Swift开源App](http://www.jianshu.com/p/a5b6d5efce88)

* [Github上的iOS App源码 (中文)](http://www.jianshu.com/p/06753d40d3d9)

* [Leancloud](https://leancloud.cn/)

* iOS 关于导航两侧按钮距离左右侧边距的修改
  - <http://www.jianshu.com/p/5c74dfc94deb>
  - <http://blog.csdn.net/woaifen3344/article/details/24793087>

* iOS 添加Xib文件，并与控制器view controller关联
  - <http://blog.csdn.net/sharmir/article/details/50606340>

* 在 iOS 应用中直接跳转到 AppStore 的方法
  - <http://blog.csdn.net/kkk0526/article/details/9836369>
  - <http://blog.csdn.net/hu_songsong/article/details/48973621>

* presentedViewController和presentingViewController的区别
  - <http://www.mamicode.com/info-detail-469709.html>

* UIImage图片处理，旋转、截取、平铺、缩放等操作，持续更新中。
  - <http://www.jianshu.com/p/9ab1205f5166>

* WKWebView的使用
  - <http://www.brighttj.com/ios/ios-wkwebview-new-features-and-use.html>
  - <http://www.jianshu.com/p/6ba2507445e4>
  - <http://www.jianshu.com/p/84a6b1ac974a>
  - <http://www.cnblogs.com/mddblog/p/5281748.html>

* iOS小技巧总结，绝对有你想要的
  - <http://www.jianshu.com/p/4523eafb4cd4>

* iOS常用动画
  - 