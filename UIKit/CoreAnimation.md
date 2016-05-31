# CoreAnimation
### 简单介绍
* Core Animation，中文翻译为核心动画，它是一组非常强大的动画处理API，使用它能做出非常炫丽的动画效果，而且往往是事半功倍。也就是说，使用少量的代码就可以实现非常强大的功能。
* Core Animation是跨平台的，可以用在Mac OS X和iOS平台。
* Core Animation的动画执行过程都是在后台操作的，不会阻塞主线程。不阻塞主线程，可以理解为在执行动画的时候还能点击（按钮）。<br/>
**要注意的是** Core Animation是直接作用在CALayer上的，并非UIView。 

### Core Animation的使用步骤

1. 使用它需要先添加QuartzCore.framework框架和引入主头文件<QuartzCore/QuartzCore.h>(iOS7不需要)

2. 初始化一个CAAnimation对象，并设置一些动画相关属性

3. 通过调用CALayer的addAnimation:forKey:方法增加CAAnimation对象到CALayer中，这样就能开始执行动画了

4. 通过调用CALayer的removeAnimationForKey:方法可以停止CALayer中的动画

##### CAAnimation
类的结构图:
![CAAnimation](http://images.cnitblog.com/i/450136/201406/211509159429975.png)
CAAnimation是所有动画类的父类，但是它不能直接使用，应该使用它的子类。

 常见属性有：

duration：动画的持续时间

repeatCount：动画的重复次数

timingFunction：控制动画运行的节奏

**说明：**     
  * 能用的动画类只有4个子类：CABasicAnimation、CAKeyframeAnimation、CATransition、CAAnimationGroup
　* CAMediaTiming是一个协议(protocol)。

CAPropertyAnimation是CAAnimation的子类，但是不能直接使用，要想创建动画对象，应该使用它的两个子类：CABasicAnimation和CAKeyframeAnimation

它有个NSString类型的keyPath属性，你可以指定CALayer的某个属性名为keyPath，并且对CALayer的这个属性的值进行修改，达到相应的动画效果。比如，指定@"position"为keyPath，就会修改CALayer的position属性的值，以达到平移的动画效果

##### 补充说明

所有动画对象的父类，负责控制动画的持续时间和速度，是个抽象类，不能直接使用，应该使用它具体的子类

属性解析：(加粗代表来自CAMediaTiming协议的属性)

** duration **：动画的持续时间

** repeatCount **：动画的重复次数

** repeatDuration **：动画的重复时间

removedOnCompletion：默认为YES，代表动画执行完毕后就从图层上移除，图形会恢复到动画执行前的状态。如果想让图层保持显示动画执行后的状态，那就设置为NO，不过还要设置fillMode为kCAFillModeForwards

** fillMode **：决定当前对象在非active时间段的行为.比如动画开始之前,动画结束之后

** beginTime **：可以用来设置动画延迟执行时间，若想延迟2s，就设置为CACurrentMediaTime()+2，CACurrentMediaTime()为图层的当前时间

timingFunction：速度控制函数，控制动画运行的节奏

delegate：动画代理


##### 参考链接
* <http://www.cnblogs.com/wendingding/p/3801036.html>



### CABasicAnimation

##### 简单介绍
CAPropertyAnimation的子类
属性解析:

fromValue：keyPath相应属性的初始值

toValue：keyPath相应属性的结束值

随着动画的进行，在长度为duration的持续时间内，keyPath相应属性的值从fromValue渐渐地变为toValue

如果fillMode=kCAFillModeForwards和removedOnComletion=NO，那么在动画执行完毕后，图层会保持显示动画执行后的状态。** 但在实质上，图层的属性值还是动画执行前的初始值，并没有真正被改变 **。

比如，CALayer的position初始值为(0,0)，CABasicAnimation的fromValue为(10,10)，toValue为(100,100)，虽然动画执行完毕后图层保持在(100,100)这个位置，实质上图层的position还是为(0,0)



##### 平移动画
代码实例
```objc
//
//  MHCoreAnimationController.m
//  MHCircularProgress
//
//  Created by apple on 16/5/31.
//  Copyright © 2016年 Mike_He. All rights reserved.
//

#import "MHCoreAnimationController.h"

@interface MHCoreAnimationController ()
@property(nonatomic ,strong) CALayer *myLayer;
@end

@implementation MHCoreAnimationController

- (void)viewDidLoad
{
    [super viewDidLoad];
    
    self.view.backgroundColor = [UIColor whiteColor];
    
    //创建layer
    CALayer *myLayer=[CALayer layer];
    //设置layer的属性
    myLayer.bounds= CGRectMake(0, 0, 50, 80);
    myLayer.backgroundColor= [UIColor yellowColor].CGColor;
    myLayer.position= CGPointMake(50, 64);
    myLayer.anchorPoint= CGPointMake(0, 0);
    myLayer.cornerRadius= 20;
    //添加layer
    [self.view.layer addSublayer:myLayer];
    self.myLayer=myLayer;
}

- (void)didReceiveMemoryWarning
{
    [super didReceiveMemoryWarning];
}

- (void) touchesBegan:(NSSet<UITouch *> *)touches withEvent:(UIEvent *)event
{
    //核心动画  平移
    [self moveViewAnimation];
}

#pragma mark - 核心动画 实现平移
- (void) moveViewAnimation
{
    // 1.创建核心动画
//    CABasicAnimation *anima = [CABasicAnimation animationWithKeyPath:@"position"];
    CABasicAnimation *anima= [CABasicAnimation animation];
    
    // 1.1告诉系统要执行什么样的动画
    anima.keyPath= @"position";
    // 设置通过动画，将layer从哪儿移动到哪儿
    anima.fromValue=[NSValue valueWithCGPoint:CGPointMake(0, 0)];
    anima.toValue = [NSValue valueWithCGPoint:CGPointMake(200, 300)];
    
    // 1.2设置动画执行完毕之后不删除动画
    anima.removedOnCompletion = NO;
    // 1.3设置保存动画的最新状态
    anima.fillMode=kCAFillModeForwards;
    
    // 2.添加核心动画到layer
    [self.myLayer addAnimation:anima forKey:nil];
}
@end

```  
代码说明：<br/>
* 设置的keyPath是@"position"，说明要修改的是CALayer的position属性，也就是会执行平移动画。也可以直接获取对应的动画对象：[CABasicAnimation animationWithKeyPath:@"position"]
* 默认情况下，动画执行完毕后，动画会自动从CALayer上移除，CALayer又会回到原来的状态。为了保持动画执行后的状态，需要设置 
    * anima.removedOnCompletion = NO;       // 1.2设置动画执行完毕之后不删除动画
    * anima.fillMode=kCAFillModeForwards;   // 1.3设置保存动画的最新状态
* byValue和toValue的区别，前者是在当前的位置上增加多少，后者是到指定的位置。

##### 缩放动画
代码实例
```objc
    // 获取动画对象
    CABasicAnimation *anima = [CABasicAnimation animationWithKeyPath:@"bounds"];
    //1.1设置动画执行时间
    anima.duration=2.0 ;
    //1.2设置动画执行完毕后不删除动画
    anima.removedOnCompletion=NO;
    //1.3设置保存动画的最新状态
    anima.fillMode=kCAFillModeForwards;
    //1.4修改属性，执行动画
    anima.toValue=[NSValue valueWithCGRect:CGRectMake(0, 0, 200, 200)];
    //2.添加动画到layer
    [self.myLayer addAnimation:anima forKey:nil];
```

##### 旋转动画
代码示例
```objc
- (void) transformViewAnimation
{
    CABasicAnimation *anima = [CABasicAnimation animationWithKeyPath:@"transform"];
    
    //1.1设置动画执行时间
    anima.duration=2.0 ;
    //1.2设置动画执行完毕后不删除动画
    anima.removedOnCompletion=NO;
    //1.3设置保存动画的最新状态
    anima.fillMode=kCAFillModeForwards;
    //1.4修改属性，执行动画
    anima.toValue=[NSValue valueWithCATransform3D:CATransform3DMakeRotation(M_PI_2+M_PI_2, 1, 1, 0)];
    //2.添加动画到layer
    [self.myLayer addAnimation:anima forKey:nil];
}
```
**提示：**如果要让图形以2D的方式旋转，只需要把CATransform3DMakeRotation在z方向上的值改为1即可。  
`anima.toValue=[NSValue valueWithCATransform3D:CATransform3DMakeRotation(M_PI_2+M_PI_4, 1, 1, 0)];`

##### 参考代码
* <http://www.cnblogs.com/wendingding/p/3801157.html>

### CAKeyframeAnimation
##### 简单介绍
是CApropertyAnimation的子类，跟CABasicAnimation的区别是：CABasicAnimation只能从一个数值(fromValue)变到另一个数值(toValue)，而CAKeyframeAnimation会使用一个NSArray保存这些数值

属性解析：

** values：**就是上述的NSArray对象。里面的元素称为”关键帧”(keyframe)。动画对象会在指定的时间(duration)内，依次显示values数组中的每一个关键帧

** path：**可以设置一个CGPathRef\CGMutablePathRef,让层跟着路径移动。path只对CALayer的anchorPoint和position起作用。如果你设置了path，那么values将被忽略

** keyTimes：**可以为对应的关键帧指定对应的时间点,其取值范围为0到1.0,keyTimes中的每一个时间值都对应values中的每一帧.当keyTimes没有设置的时候,各个关键帧的时间是平分的

说明：CABasicAnimation可看做是最多只有2个关键帧的CAKeyframeAnimation


代码示例:
```objc
    //1.创建核心动画
    CAKeyframeAnimation *keyAnima=[CAKeyframeAnimation animation];
    //平移
    keyAnima.keyPath=@"position";
    //1.1告诉系统要执行什么动画
    NSValue *value1=[NSValue valueWithCGPoint:CGPointMake(100, 100)];
    NSValue *value2=[NSValue valueWithCGPoint:CGPointMake(200, 100)];
    NSValue *value3=[NSValue valueWithCGPoint:CGPointMake(200, 200)];
    NSValue *value4=[NSValue valueWithCGPoint:CGPointMake(100, 200)];
    NSValue *value5=[NSValue valueWithCGPoint:CGPointMake(100, 100)];
    keyAnima.values=@[value1,value2,value3,value4,value5];
    //1.2设置动画执行完毕后，不删除动画
    keyAnima.removedOnCompletion=NO;
    //1.3设置保存动画的最新状态
    keyAnima.fillMode=kCAFillModeForwards;
    //1.4设置动画执行的时间
    keyAnima.duration=4.0;
    //1.5设置动画的节奏
    keyAnima.timingFunction=[CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseInEaseOut];
    
    //设置代理，开始—结束
//    keyAnima.delegate=self;
    //2.添加核心动画
    [self.myLayer addAnimation:keyAnima forKey:nil];
```

补充：设置动画的节奏

 ![](http://images.cnitblog.com/i/450136/201406/211931059267032.png)
 
 
 使用path）让layer在指定的路径上移动（画圆）：
 ```objc
  //1.创建核心动画
    CAKeyframeAnimation *keyAnima=[CAKeyframeAnimation animation];
    //平移
    keyAnima.keyPath=@"position";
    //1.1告诉系统要执行什么动画
    //创建一条路径
    CGMutablePathRef path=CGPathCreateMutable();
    //设置一个圆的路径
    CGPathAddEllipseInRect(path, NULL, CGRectMake(150, 100, 100, 100));
    
    keyAnima.path=path;
    
    //有create就一定要有release
    CGPathRelease(path);
    //1.2设置动画执行完毕后，不删除动画
    keyAnima.removedOnCompletion=NO;
    //1.3设置保存动画的最新状态
    keyAnima.fillMode=kCAFillModeForwards;
    //1.4设置动画执行的时间
    keyAnima.duration=5.0;
    //1.5设置动画的节奏
    keyAnima.timingFunction=[CAMediaTimingFunction functionWithName:kCAMediaTimingFunctionEaseInEaseOut];
    
    //设置代理，开始—结束
//    keyAnima.delegate=self;
    //2.添加核心动画
    [self.myLayer addAnimation:keyAnima forKey:nil];
 ```
 **说明**：可以通过path属性，让layer在指定的轨迹上运动。



//停止self.customView.layer上名称标示为wendingding的动画
` [self.customView.layer removeAnimationForKey:@"#动画名称#"];`

##### 图片抖动
代码示例：
```objc
//1.创建核心动画
    CAKeyframeAnimation *keyAnima=[CAKeyframeAnimation animation];
    keyAnima.keyPath=@"transform.rotation";
    //设置动画时间
    keyAnima.duration=0.1;
    //设置图标抖动弧度
    //把度数转换为弧度  度数/180*M_PI
    keyAnima.values=@[@(-angle2Radian(4)),@(angle2Radian(4)),@(-angle2Radian(4))];
    //设置动画的重复次数(设置为最大值)
    keyAnima.repeatCount=MAXFLOAT;
    
    keyAnima.fillMode=kCAFillModeForwards;
    keyAnima.removedOnCompletion=NO;
    //2.添加动画
    [self.myLayer addAnimation:keyAnima forKey:nil];
```

##### 参考链接
* <http://www.cnblogs.com/wendingding/p/3801330.html>


### CATransition 转场动画
CAAnimation的子类，用于做转场动画，能够为层提供移出屏幕和移入屏幕的动画效果。iOS比Mac OS X的转场动画效果少一点

UINavigationController就是通过CATransition实现了将控制器的视图推入屏幕的动画效果

属性解析:

type：动画过渡类型

subtype：动画过渡方向

startProgress：动画起点(在整体动画的百分比)

endProgress：动画终点(在整体动画的百分比)


代码示例：
```objc
//1.创建核心动画
    CATransition *ca=[CATransition animation];
    
    //1.1告诉要执行什么动画
    //1.2设置过度效果
    ca.type=@"cube";
    //1.3设置动画的过度方向（向右）
    ca.subtype=kCATransitionFromRight;
    //1.4设置动画的时间
    ca.duration=2.0;
    //1.5设置动画的起点
    ca.startProgress=0.5;
    //1.6设置动画的终点
//    ca.endProgress=0.5;
    
    //2.添加动画
    [self.iconView.layer addAnimation:ca forKey:nil];
```


```objc
CATransition比较强大，一般可以使用CATransition模拟UIView的动画。

/* 过渡效果
fade     //交叉淡化过渡(不支持过渡方向)
push     //新视图把旧视图推出去
moveIn   //新视图移到旧视图上面
reveal   //将旧视图移开,显示下面的新视图
cube     //立方体翻滚效果
oglFlip  //上下左右翻转效果
suckEffect   //收缩效果，如一块布被抽走(不支持过渡方向)
rippleEffect //滴水效果(不支持过渡方向)
pageCurl     //向上翻页效果
pageUnCurl   //向下翻页效果
cameraIrisHollowOpen  //相机镜头打开效果(不支持过渡方向)
cameraIrisHollowClose //相机镜头关上效果(不支持过渡方向)
*/
 
/* 过渡方向
fromRight;
fromLeft;
fromTop;
fromBottom;
*/

CATransition *animation = [CATransition animation];
animation.delegate = self;
animation.duration = 0.5f; //动画时长
animation.timingFunction = UIViewAnimationCurveEaseInOut;
animation.fillMode = kCAFillModeForwards;
animation.type = @”cube”; //过度效果
animation.subtype = @”formLeft”; //过渡方向
animation.startProgress = 0.0 //动画开始起点(在整体动画的百分比)
animation.endProgress = 1.0;  //动画停止终点(在整体动画的百分比)
animation.removedOnCompletion = NO;
[self.view.layer addAnimation:animation forKey:@"animation"];


```

##### 参考链接
* <http://www.cnblogs.com/wendingding/p/3801454.html>
* <http://www.cnblogs.com/pengyingh/articles/2339420.html>



### CAAnimationGroup 组动画
CAAnimation的子类，可以保存一组动画对象，将CAAnimationGroup对象加入层后，组中所有动画对象可以同时并发运行

属性解析：

animations：用来保存一组动画对象的NSArray

默认情况下，一组动画对象是同时运行的，也可以通过设置动画对象的beginTime属性来更改动画的开始时间


```objc
// 平移动画
    CABasicAnimation *a1 = [CABasicAnimation animation];
    a1.keyPath = @"transform.translation.y";
    a1.toValue = @(100);
    // 缩放动画
    CABasicAnimation *a2 = [CABasicAnimation animation];
    a2.keyPath = @"transform.scale";
    a2.toValue = @(0.0);
    // 旋转动画
    CABasicAnimation *a3 = [CABasicAnimation animation];
    a3.keyPath = @"transform.rotation";
    a3.toValue = @(M_PI_2);
    
    // 组动画
    CAAnimationGroup *groupAnima = [CAAnimationGroup animation];
    
    groupAnima.animations = @[a1, a2, a3];
    
    //设置组动画的时间
    groupAnima.duration = 2;
    groupAnima.fillMode = kCAFillModeForwards;
    groupAnima.removedOnCompletion = NO;
    
    [self.iconView.layer addAnimation:groupAnima forKey:nil];
```


##### 参考链接
* <http://www.csdn123.com/html/blogs/20131107/94198.htm>

