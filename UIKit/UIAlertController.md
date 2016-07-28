# UIAlertController

---

## 开篇扯淡

在iOS8中，新增了UIAlertController，它可以同时实现Alert和Action Sheets，并且接口采用block方式，它将在应用的同一个window中展示，而不是之前的新window中展示，它还具有和之前的popover controller相同的实现方式，通过presentViewController来展示。

## 区别

1. UIAlertView  iOS系统为了保证UIAlertView在所有界面之上，它会临时创建一个新的UIWindow，通过将UIWindow的UIWindowLevel设置的更高，让UIAlertView盖在所有应用的界面之上          

2. UIAlertController  是继承自UIViewController，它采用一个UIPopoverPresentationController类进行管理，UIPopoverPresentationController又继承自 UIPresentationController，其中的presentingViewController属性表示展示之前的Controller，presentedViewController属性表示被展示的Controller。另外这种方式，也统一了iPhone和iPad的使用方式


## 参考链接
* [iOS开发 UIAlertController的创建与使用](* http://jingyan.baidu.com/article/e9fb46e17164757521f76698.html)
* [在iOS 8中使用UIAlertController](http://www.cocoachina.com/ios/20141126/10320.html)
* [[iOS]改变UIAlertController的标题、内容的字体和颜色](http://www.jianshu.com/p/51949eec2e9c)
* 