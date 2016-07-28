# Cache
---
##NSCache

NSCache 是苹果官方提供的缓存类，用法与 NSMutableDictionary 的用法很相似，在 AFNetworking 和 SDWebImage 中，使用它来管理缓存

NSCache 在系统内存很低时，会自动释放一些对象

备注：这句话源自苹果的官方文档，不过在模拟器中模拟内存警告时，缓存不会做清理动作 为了确保接收到内存警告时能够真正释放内存，最好调用一下 removeAllObjects 方法
NSCache 是线程安全的，在多线程操作中，不需要对 Cache 加锁

NSCache 的 Key 只是做强引用，不需要实现 NSCopying 协议

属性

name delegate 
totalCostLimit
缓存空间的最大总成本，超出上限会自动回收对象 默认值是 0，表示没有限制
countLimit

能够缓存对象的最大数量 默认值是 0，表示没有限制  

evictsObjectsWithDiscardedContent
标示缓存是否回收废弃的内容 默认值是 YES，表示自动回收
方法

-objectForKey: 返回与键值关联的对象 -setObject:forKey:
在缓存中设置指定键名对应的值 与可变字典不同，缓存对象不会对键名做 copy 操作 0 成本 -setObject:forKey:cost:
在缓存中设置指定键名对应的值，并且指定该键值对的成本 成本 (cost) 用于计算记录在缓冲中的所有对象的总成本
置对象并指定”成本”，成本可以自行指定
啥叫成本？
例子：缓存图片 缓存 100 张图片 将图片的”宽 * 高”当作成本，图像”像素” 10M 当作缓存成本，无论缓存的多少张照片，只要像素值超过 10M，就自动清理 缓存图像的时候，使用成本，比单纯设置数量要科学！
(void)setObject:(id)obj forKey:(id)key cost:(NSUInteger)g;

当出现内存警告时，或者超出缓存的总成本上限时，缓存会开启一个回收过程，删除部分元素

-removeObjectForKey:

删除缓存中，指定键名的对象

-removeAllObjects

删除缓存中所有对象（很可怕，最好别用）
委托方法

cache:willEvictObject
缓存将要删除对象时调用 不能在此方法中修改缓存


## 参考链接
* [iOS---NSCache的简单使用
](http://www.2cto.com/kf/201503/385497.html)

* [Objective-C中的缓存](http://www.15yan.com/topic/yi-dong-kai-fa-na-dian-shi/45toOUzFGlr/)