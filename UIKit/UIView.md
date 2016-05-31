# UIView CALayer
### UIView和CALayer的选择
* 如果显示出来的东西需要跟用户进行交互的话，用UIView；如果不需要跟用户进行交互，用UIView或者CALayer都可以.当然，CALayer的性能会高一些，因为它少了事件处理的功能，更加轻量级 。
* CALayer是定义在QuartzCore框架中的；CGImageRef、CGColorRef两种数据类型是定义在CoreGraphics框架中的；UIColor、UIImage是定义在UIKit框架中的其次，QuartzCore框架和CoreGraphics框架是可以跨平台使用的，在iOS和Mac OS X上都能使用，但是UIKit只能在iOS中使用。因此，为了保证可移植性，QuartzCore不能使用UIImage、UIColor，只能使用CGImageRef、CGColorRef不过很多情况下，可以通过UIKit对象的特定方法，得到CoreGraphics对象，比如UIImage的CGImage方法可以返回一个CGImageRef。



### 参考链接
* <http://www.cnblogs.com/wendingding/p/3800736.html>