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
* 画第一条线的时候，会把当前的图形上下文拷贝一份保存到图形上下文栈中。
* 画第二条线的时候，去图形上下文栈中取出栈顶的绘图信息，作为第二条线的状态信息，第二条线的状态信息也是据此（最初保存的那份图形上下文）进行绘制。
* **注意：** 在栈里保存了几次，那么就可以取几次（比如不能保存了1次，取两次，在取第二次的时候，栈里为空会直接挂掉）。
