# Quartz2D

### Quartz2D 绘图
画线的三个步骤：
1. 获取上下文
2. 绘图
3. 渲染

 参考链接：<http://www.cnblogs.com/wendingding/p/3782489.html>

### Quartz2D 细节
图形上下文栈：<br>
程序启动，显示自定义的view。当程序第一次显示在我们眼前的时候，程序会调用drawRect:方法，在里面获取了图形上下文（在内存中拥有了），然后利用图形上下文保存绘图信息，可以理解为图形上下文中有一块区域用来保存绘图信息，有一块区域用来保存绘图的状态（线宽，圆角，颜色）。直线不是直接绘制到view上的，可以理解为在图形上下文中有一块单独的区域用来先绘制图形，当调用渲染方法的时候，再把绘制好的图形显示到view上去。
 
在绘制图形区域，会去保存绘图状态区域中查找对应的状态信息（线宽，圆角，颜色），然后在绘图区域把对第一条直线绘制完成。其实在渲染之前，就已经把直线在绘制图形区域画好了。


在获取图形上下文之后，通过 CGContextSaveGState(ctx); 方法，把当前获取的上下文拷贝一份，保存一份最纯洁的图形上下文。
在画第二条线之前，使用CGContextRestoreGState(ctx);方法，还原开始的时候保存的那份最纯洁的图形上下文。

```objc
- (void)drawRect:(CGRect)rect
  {
      //获取上下文
      CGContextRef ctx=UIGraphicsGetCurrentContext();
      //保存一份最初的图形上下文
      CGContextSaveGState(ctx);
      
      //绘图
      //第一条线
     CGContextMoveToPoint(ctx, 20, 100);
     CGContextAddLineToPoint(ctx, 100, 320);
     
     //设置第一条线的状态
     //设置线条的宽度
     CGContextSetLineWidth(ctx, 12);
     //设置线条的颜色
     [[UIColor brownColor]set];
     //设置线条两端的样式为圆角
     CGContextSetLineCap(ctx,kCGLineCapRound);
     //对线条进行渲染
     CGContextStrokePath(ctx);
     
     //还原开始的时候保存的那份最纯洁的图形上下文
     CGContextRestoreGState(ctx);
     //第二条线
     CGContextMoveToPoint(ctx, 40, 200);
     CGContextAddLineToPoint(ctx, 80, 100);
     
     //清空状态
 //    CGContextSetLineWidth(ctx, 1);
 //    [[UIColor blackColor]set];
 //    CGContextSetLineCap(ctx,kCGLineCapButt);
     
     //渲染
     CGContextStrokePath(ctx);
}
```

### 图形上下文栈机制
* 画第一条线的时候，会把当前的图形上下文拷贝一份保存到** 图形上下文栈 **中。
* 画第二条线的时候，去图形上下文栈中取出栈顶的绘图信息，作为第二条线的状态信息，第二条线的状态信息也是据此（最初保存的那份图形上下文）进行绘制。
* **注意：** 在栈里保存了几次，那么就可以取几次（比如不能保存了1次，取两次，在取第二次的时候，栈里为空会直接挂掉）。


### 绘图相关
* drawRect:方法不能由我们自己手动调用，只能由系统来调用。
* drawRect:调用的时机：当第一次显示或者一个重绘事件发生时调用。
* setNeedsDisplay方法：重新绘制，调用这个方法就会通知自定义的view重新绘制画面，调用drawRect:。
* **提示：**当一个view从xib或storyboard创建出来时，会调用awakefromnib方法。

### Tips:
##### 下面两个方法的调用顺序
``` objc
-(void)awakeFromNib
-(id)initWithCoder:(NSCoder *)aDecoder
```
**提示：**  
* 如果view是从xib或storyboard中创建可以调用awakefromnib方法。  
* 归档。从文件创建view，其实会先调用initwithcoder这个方法。xib和storyboard也是文件。

上面两个方法，`-(id)initWithCoder:(NSCoder *)aDecoder`会先调用。实现该方法需要实现NSCoding协议，由于创建的UIView默认就已经实现了该协议。

##### 两个定时器
* 第一个：  
`
[NSTimer scheduledTimerWithTimeInterval:0.1 target:self selector:@selector(updateImage) userInfo:nil repeats:YES];
`  
** 说明：** NSTimer一般用于定时的更新一些非界面上的数据,告诉多久调用一次

* 第二个：  
```objc
        CADisplayLink *display= [CADisplayLink displayLinkWithTarget:self selector:@selector(updateImage)];
        [display addToRunLoop:[NSRunLoopmainRunLoop] forMode:NSDefaultRunLoopMode];
```  
** 说明：** CADisplayLink刷帧，默认每秒刷新60次。该定时器创建之后，默认是不会执行的，需要把它加载到消息循环中


### Quartz2D使用（绘图路径）
##### 绘图路径
1. 创建路径  cgmutablepathref 调用该方法相当于创建了一个路径，这个路径用来保存绘图信息。
2. 把绘图信息添加到路径里边。以前的方法是点的位置添加到ctx（图形上下文信息）中，ctx 默认会在内部创建一个path用来保存绘图信息。在图形上下文中有一块存储空间专门用来存储绘图信息，其实这块空间就是CGMutablePathRef。
3. 把路径添加到上下文中。


context绘图
```objc
    //1.获取图形上下文
    CGContextRef ctx=UIGraphicsGetCurrentContext();
    //2.绘图（画线）
    //设置起点
    CGContextMoveToPoint(ctx, 20, 20);
    //设置终点
    CGContextAddLineToPoint(ctx, 200, 300);
    //渲染
    CGContextStrokePath(ctx);
```

路径方法
```objc
//1.获取图形上下文
    CGContextRef ctx=UIGraphicsGetCurrentContext();
    
    //2.绘图
    //2.1创建一条直线绘图的路径
    //注意：但凡通过Quartz2D中带有creat/copy/retain方法创建出来的值都必须要释放
    CGMutablePathRef path=CGPathCreateMutable();
    //2.2把绘图信息添加到路径里
    CGPathMoveToPoint(path, NULL, 20, 20);
    CGPathAddLineToPoint(path, NULL, 200, 300);
    //2.3把路径添加到上下文中
    //把绘制直线的绘图信息保存到图形上下文中
    CGContextAddPath(ctx, path);
    
    //3.渲染
    CGContextStrokePath(ctx);
    
    //4.释放前面创建的两条路径
    //第一种方法
    CGPathRelease(path);
    //第二种方法
    //    CFRelease(path);
}
```
** 说明 ** 上面两个代码是等价的。  
使用路径绘图可读性比较好，便于区分。使用path，则一个path就代表一条路径。绘制多个图形的情况下，建议使用Path来绘制。
```objc
- (void)drawRect:(CGRect)rect
{
    //1.获取图形上下文
    CGContextRef ctx=UIGraphicsGetCurrentContext();

    //2.绘图
    //2.a 画一条直线
    //2.a.1创建一条绘图的路径
    //注意：但凡通过Quartz2D中带有creat/copy/retain方法创建出来的值都必须要释放
    CGMutablePathRef path=CGPathCreateMutable();
    
    //2.a.2把绘图信息添加到路径里
    CGPathMoveToPoint(path, NULL, 20, 20);
    CGPathAddLineToPoint(path, NULL, 200, 300);
    
    //2.a.3把路径添加到上下文中
    //把绘制直线的绘图信息保存到图形上下文中
    CGContextAddPath(ctx, path);
    
    
    //2.b画一个圆
    //2.b.1创建一条画圆的绘图路径(注意这里是可变的，不是CGPathRef)
    CGMutablePathRef path1=CGPathCreateMutable();
    
    //2.b.2把圆的绘图信息添加到路径里
    CGPathAddEllipseInRect(path1, NULL, CGRectMake(50, 50, 100, 100));
    
    //2.b.3把圆的路径添加到图形上下文中
    CGContextAddPath(ctx, path1);
    
    
    //3.渲染
    CGContextStrokePath(ctx);
    
    //4.释放前面创建的两条路径
    //第一种方法
    CGPathRelease(path);
    CGPathRelease(path1);
    //第二种方法
//    CFRelease(path);
}
```
**提示：**如果是画线，那么就创建一条路径（path）用来保存画线的绘图信息，如果又要重新画一个圆，那么就可以创建一条新的路径来专门保存画圆的绘图信息。  
**注意：**
但凡通过quarzt2d中带有`creat/copy/retain`方法创建出来的值都必须手动的释放
有两种方法可以释放前面创建的路径：
```objc
 CGPathRelease(path);
 CFRelease(path);  
```
**说明**：CFRelease属于更底层的cocafoundation框架


### 补充知识点
画四边形的一些方法：
1. 通过连接固定的点绘制四边形
2. 指定起点和宽高绘制四边形
3. 把第二种方式中的两步合并成一步。
4. 绘制实心的四边形，注意没有空心的方法
5. 画根线，设置线条的宽度（通过这种方式可以画斜的四边形）

```objc
- (void)drawRect:(CGRect)rect
{
    //获取图形上下文
    CGContextRef ctx=UIGraphicsGetCurrentContext();
    //第一种画法,通过连接固定的点绘制四边形
//    CGContextMoveToPoint(ctx, 0, 20);
//    CGContextAddLineToPoint(<#CGContextRef c#>, <#CGFloat x#>, <#CGFloat y#>);
//    CGContextAddLineToPoint(<#CGContextRef c#>, <#CGFloat x#>, <#CGFloat y#>);
//    CGContextAddLineToPoint(<#CGContextRef c#>, <#CGFloat x#>, <#CGFloat y#>);
    
    //第二种方式：指定起点和宽高绘制四边形
//    CGContextAddRect(ctx, CGRectMake(20, 20, 200, 100));
//    //渲染
//    CGContextStrokePath(ctx);
    
    //第三种方式：二种的两步合并成一步。
    //画空心的四边形
//    CGContextStrokeRect(ctx, CGRectMake(20, 20, 200, 100));
//    //画实心的四边形
//    CGContextFillRect(ctx, CGRectMake(20, 20, 200, 100));
    
    //第四种方式（oc的方法）：绘制实心的四边形，注意没有空心的方法
    UIRectFill(CGRectMake(20, 20, 200, 100));
    
    //第五种方式：画根线，设置线条的宽度（通过这种方式可以画斜的四边形）
//    CGContextMoveToPoint(ctx, 20, 20);
//    CGContextAddLineToPoint(ctx, 100, 200);
//    CGContextSetLineWidth(ctx, 50);
//    //注意，线条只能画成是空心的
//    CGContextStrokePath(ctx);
    
}
```




























