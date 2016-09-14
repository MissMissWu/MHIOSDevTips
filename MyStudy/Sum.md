# Sum

```objc
Mike_He_Account

**open**
password：1234


** 个推 **
https://dev.getui.com/dos4.0/index.html#login

account：61txw    
password： #123456C#


**AppId**
https://developer.apple.com/

account:    tongxunnetwork@126.com
password:  Tongxun2016@

**BugFree**
http://192.168.0.20:7010/bugfree3.0.4/index.php/site/login

account：heqy 
password：1234567

**今目标**
account：heqianyuan@7196050
password：12345678

**SVN**
account：ios2
password：1234567

**WIFI**
account：Edit
password：asdfghjkl

**企业邮箱**
account：heqy@sznobel.com
password：123456


** 网易邮箱 **
account : tongxunnetwork@126.com
password: 0987654321

** 椅子唯一标识 **
YZ - 0123

hgs202 a73294



源代码svn仓库地址
https://112.74.99.76/svn/iOS_Code


http://www.cocoachina.com/ios/20151217/14668.html

清除xcode缓存：/Users/Apple/Library/Developer/Xcode/DerivedData



我的学习经验：
iOS9
<key>NSAppTransportSecurity</key>

    <dict>

        <key>NSAllowsArbitraryLoads</key>

        <true/>

    </dict>



1.#warning 千万不要这么写------------会导致你pop到上一个界面出现崩溃 而且不提供任何信息
- (void)scrollViewDidScroll:(UIScrollView *)scrollView
{

    if (self.mySearchBar.isFirstResponder)

    {

        [self.mySearchBar resignFirstResponder];

    }

}



2.ios7以后  设置导航栏的背景图片 需要保证图片的高度是64  否则会影响view的布局  主要取决于导航栏的透明度  90%即可



3.- (void)dealloc

{

    //好习惯

    if (self.timer.isValid) {

        [self.timer invalidate];

        self.timer=nil;

    }

}



4.//解决触控点击事件和手势的冲突

- (BOOL)gestureRecognizer:(UIGestureRecognizer *)gestureRecognizer shouldReceiveTouch:(UITouch *)touch

{

    // 若为UITableViewCellContentView（即点击了tableViewCell），则不截获Touch事件

    if ([NSStringFromClass([touch.view class]) isEqualToString:@"UITableViewCellContentView"]) {

        return NO;

    }

    return YES;

}



5.- (NSIndexPath *)indexPathForCell:(UITableViewCell *)cell;  // returns nil if cell is not visible



6.安装cocoal pods （百度有教程）

步骤一：如何在Mac OS X上安装 Ruby运行环境

步骤二：安装CocoaPods

步骤三：新建项目并在工程根目录下新建Podfile文件，配置需要管理的第三方库

步骤四：运行pod install下载安装第三方库

pod install  换成pod install --verbose --no-repo-update这个命令，前面的命令被墙了 ,
pod update --verbose --no-repo-update
同理

7.http://www.versionsapp.com/              SVN：Versions工具包

8.int pageCount = (recordCount - 1) / pageSize + 1;
(30-1)/5 + 1 = 6
(31-1)/5 + 1 = 7
(29-1)/5 + 1 = 6

9.归档
上一级包含下一级，归档上一级时，必须下一级也得归档，必须实现NSCoding的方法 
eg：上一级：Menus模型 ——menus数组里面装的都是下一级 menuModel模型  则MenuModel模型必须实现NSCoding的方法 否则崩溃

10. 程序退出
exit(0);

11.//利用KVC设置私有变量

    [item3 setValue:[NSValue valueWithUIEdgeInsets:UIEdgeInsetsMake(0, 0, 0, 0)] forKeyPath:@"imageInsets”];



12.

Xcode6.3插件失效解决办法   

1.打开终端，输入以下代码获取到DVTPlugInCompatibilityUUID
       defaults read /Applications/Xcode.app/Contents/Info DVTPlugInCompatibilityUUID

2.然后输入如下命令   【最后一项是获取到的DVTPlugInCompatibilityUUID】
     find ~/Library/Application\ Support/Developer/Shared/Xcode/Plug-ins -name Info.plist -maxdepth 3 | xargs -I{} defaults write {} DVTPlugInCompatibilityUUIDs -array-add 9F75337B-21B4-4ADC-B558-F9CADF7073A7

13.UITableViewCell 或者 UICollectionViewCell  添加长按手势  最好的办法是将长按手势添加到UITableView或者UICollectionView身上 切记不要添加到cell身上 切记切记。。
eg:
#pragma mark - 添加手势执行的方法
-(void)longPressToDo:(UILongPressGestureRecognizer *)gesture

{

    if (gesture.state == UIGestureRecognizerStateBegan)

    {

        CGPoint point = [gesture locationInView:self.collectionView];

        self.indexPath = [self.collectionView indexPathForItemAtPoint:point];

        MyLog(@"--item is--%ld ---section is ---%ld" , self.indexPath.item , self.indexPath.section);

        if (self.indexPath.item==0) {

            //1.添加照片

            [self addNewPictuers];

        }else{

            //2.修改或者删除照片

            [self dealWithCurrentPicture];

        }

    }

}


14.不要随意改动第三方的框架 尊重他人劳动成果。

15.
NSString * bundlePath = [[ NSBundle mainBundle] pathForResource: @ "MyBundle"ofType :@ "bundle"];

NSBundle *resourceBundle = [NSBundle bundleWithPath:bundlePath];

UIViewController *vc = [[UIViewController alloc] initWithNibName:@"vc_name"bundle:resourceBundle];



图片获得bundle中的资源
UIImageView *imgView=[[UIImageView alloc] initWithFrame:CGRectMake(50, 50, 50,50)];

UIImage *image = [UIImage imageNamed:@"MyBundle.bundle/img_collect_success"];

[imgView setImage:image];


或者

UIImageView *imgView=[[UIImageView alloc] initWithFrame:CGRectMake(50, 50, 50,50)];

NSString *imgPath= [bundlePath stringByAppendingPathComponent:@"img_collect_success.png"];

UIImage *image_1=[UIImage imageWithContentsOfFile:imgPath];

[imgView setImage:image_1];


当然，可以写成预编译语句：
#define MYBUNDLE_NAME @ "MyBundle.bundle"

#define MYBUNDLE_PATH [[[NSBundle mainBundle] resourcePath] stringByAppendingPathComponent: MYBUNDLE_NAME]

#define MYBUNDLE [NSBundle bundleWithPath: MYBUNDLE_PATH]


注意：
---bundle本质上就是一个目录，里面可以存放各种资源，比如图片，xib等等。
---简单的做法是：建立一个目录，把你的图片放进去，将目录重命名为xxx.bundle，然后就库在代码中读取图片资源了.
 比如要读取user.bundle 中的alert.png图片：
 UIImage *img = [UIImage imageNamed:@"user.bundle/alert.png"];

 还要注意的是如果要删除、修改和添加图片，需要把bundle改回为文件夹，然后改动完后再修改回去才行。



16.最后需要将cell的高度返回

-(CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath方法：

-(CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath

{  

    TableViewCell *cell = [self tableView:_tableView cellForRowAtIndexPath:indexPath];  

   return cell.frame.size.height;  

}  



18.设置cell为圆角

#pragma mark - Table view data source
- (void)tableView:(UITableView *)tableView willDisplayCell:(UITableViewCell *)cell forRowAtIndexPath:(NSIndexPath *)indexPath
{
    if ([cell respondsToSelector:@selector(tintColor)]) {
        if (tableView == self.tabelView)
        {
            CGFloat cornerRadius = 5.f;
            cell.backgroundColor = UIColor.clearColor;
            CAShapeLayer *layer = [[CAShapeLayer alloc] init];
            CGMutablePathRef pathRef = CGPathCreateMutable();
            CGRect bounds = CGRectInset(cell.bounds, 5, 0);
            BOOL addLine = NO;
            if (indexPath.row == 0 && indexPath.row == [tableView numberOfRowsInSection:indexPath.section]-1) {
                CGPathAddRoundedRect(pathRef, nil, bounds, cornerRadius, cornerRadius);
            } else if (indexPath.row == 0) {
                CGPathMoveToPoint(pathRef, nil, CGRectGetMinX(bounds), CGRectGetMaxY(bounds));
                CGPathAddArcToPoint(pathRef, nil, CGRectGetMinX(bounds), CGRectGetMinY(bounds), CGRectGetMidX(bounds), CGRectGetMinY(bounds), cornerRadius);
                CGPathAddArcToPoint(pathRef, nil, CGRectGetMaxX(bounds), CGRectGetMinY(bounds), CGRectGetMaxX(bounds), CGRectGetMidY(bounds), cornerRadius);
                CGPathAddLineToPoint(pathRef, nil, CGRectGetMaxX(bounds), CGRectGetMaxY(bounds));
                addLine = YES;
            } else if (indexPath.row == [tableView numberOfRowsInSection:indexPath.section]-1)
            {
                CGPathMoveToPoint(pathRef, nil, CGRectGetMinX(bounds), CGRectGetMinY(bounds));
                CGPathAddArcToPoint(pathRef, nil, CGRectGetMinX(bounds), CGRectGetMaxY(bounds), CGRectGetMidX(bounds), CGRectGetMaxY(bounds), cornerRadius);
                CGPathAddArcToPoint(pathRef, nil, CGRectGetMaxX(bounds), CGRectGetMaxY(bounds), CGRectGetMaxX(bounds), CGRectGetMidY(bounds), cornerRadius);
                CGPathAddLineToPoint(pathRef, nil, CGRectGetMaxX(bounds), CGRectGetMinY(bounds));
            } else {
                CGPathAddRect(pathRef, nil, bounds);
                addLine = YES;
            }
            layer.path = pathRef;
            CFRelease(pathRef);
            layer.fillColor = [UIColor colorWithWhite:1.f alpha:0.8f].CGColor;
            
            if (addLine == YES)
            {
                CALayer *lineLayer = [[CALayer alloc] init];
                CGFloat lineHeight = (1.f / [UIScreen mainScreen].scale);
                lineLayer.frame = CGRectMake(CGRectGetMinX(bounds)+10, bounds.size.height-lineHeight, bounds.size.width-10, lineHeight);
                lineLayer.backgroundColor = tableView.separatorColor.CGColor;
                [layer addSublayer:lineLayer];
            }
            UIView *testView = [[UIView alloc] initWithFrame:bounds];
            [testView.layer insertSublayer:layer atIndex:0];
            testView.backgroundColor = UIColor.clearColor;
            cell.backgroundView = testView;
        }
    }
}


19.- (void)setPlacehoder:(NSString *)placehoder
{

#warning 如果是copy策略，setter最好这么写

    _placehoder = [placehoder copy];

    // 设置文字

    self.placehoderLabel.text = placehoder;

    // 重新计算子控件的fame

    [self setNeedsLayout];

}

20.当你把 self.passwordTextField.secureTextEntry=YES;的话,系统自动就会调用系统的键盘.第三方会被禁用



21.添加刚刚创建的pch文件的工程路径，添加格式：“$(SRCROOT)/项目名称/pch文件名” 

eg:$(SRCROOT)/TXZS/Prefix.pch



22.[zhuan] svn is already under version control问题解决

svn ci 时出现 xx is already under version control，然后无法提交，出现这个问题的原因是你所提交的文件或目录是其他SVN的东西，即下面有.svn的目录，需要先把它们删除才能提交，具体操作如下：

打开terminal，cd到你新增加的那个目录，然后用下面的命令

#find . -mindepth 2 -name '.svn' -exec rm -rf '{}' \;
这个命令会递归的删除目录下所有.svn的文件夹，现在，再提交一次试试？

.svn 直接删除也可以



23.常用正则表达式 整理篇

http://www.jb51.net/article/17355.htm

正则表达式高级学习技巧
http://www.jb51.net/article/9229.htm

//正则表达式
http://www.jb51.net/article/18526.htm

24 ios坐标系转换
// 将像素point由point所在视图转换到目标视图view中，返回在目标视图view中的像素值  
- (CGPoint)convertPoint:(CGPoint)point toView:(UIView *)view;  
// 将像素point从view中转换到当前视图中，返回在当前视图中的像素值  
- (CGPoint)convertPoint:(CGPoint)point fromView:(UIView *)view;  
  
// 将rect由rect所在视图转换到目标视图view中，返回在目标视图view中的rect  
- (CGRect)convertRect:(CGRect)rect toView:(UIView *)view;  
// 将rect从view中转换到当前视图中，返回在当前视图中的rect  
- (CGRect)convertRect:(CGRect)rect fromView:(UIView *)view;

注：若view参数为空，则转换为窗口（window）的坐标系；接收者与view都必须是同一窗口（window）的对象。
  
例把UITableViewCell中的subview(btn)的frame转换到 controllerA中

// controllerA 中有一个UITableView, UITableView里有多行UITableVieCell，cell上放有一个button  

// 在controllerA中实现:  

CGRect rc = [cell convertRect:cell.btn.frame toView:self.view];  

或  

CGRect rc = [self.view convertRect:cell.btn.frame fromView:cell];  

// 此rc为btn在controllerA中的rect    

或当已知btn时：  

CGRect rc = [btn.superview convertRect:btn.frame toView:self.view];  

或  

CGRect rc = [self.view convertRect:btn.frame fromView:btn.superview];  


25.
UIView常用的一些方法小记之setNeedsDisplay和setNeedsLayout

1,UIView的setNeedsDisplay和setNeedsLayout方法

  首先两个方法都是异步执行的。而setNeedsDisplay会调用自动调用drawRect方法，这样可以拿到  UIGraphicsGetCurrentContext，就可以画画了。而setNeedsLayout会默认调用layoutSubViews，

 就可以  处理子视图中的一些数据。

综上所诉，setNeedsDisplay方便绘图，而layoutSubViews方便出来数据。

layoutSubviews在以下情况下会被调用：

1、init初始化不会触发layoutSubviews。

2、addSubview会触发layoutSubviews。

3、设置view的Frame会触发layoutSubviews，当然前提是frame的值设置前后发生了变化。

4、滚动一个UIScrollView会触发layoutSubviews。

5、旋转Screen会触发父UIView上的layoutSubviews事件。

6、改变一个UIView大小的时候也会触发父UIView上的layoutSubviews事件。

7、直接调用setLayoutSubviews。



drawRect在以下情况下会被调用：

 1、如果在UIView初始化时没有设置rect大小，将直接导致drawRect不被自动调用。drawRect调用是在Controller->loadView, Controller->viewDidLoad 两方法之后掉用的.所以不用担心在控制器中,这些View的drawRect就开始画了.这样可以在控制器中设置一些值给View(如果这些View draw的时候需要用到某些变量值).

2、该方法在调用sizeToFit后被调用，所以可以先调用sizeToFit计算出size。然后系统自动调用drawRect:方法。

3、通过设置contentMode属性值为UIViewContentModeRedraw。那么将在每次设置或更改frame的时候自动调用drawRect:。

4、直接调用setNeedsDisplay，或者setNeedsDisplayInRect:触发drawRect:，但是有个前提条件是rect不能为0。

以上1,2推荐；而3,4不提倡



drawRect方法使用注意点：

1、若使用UIView绘图，只能在drawRect：方法中获取相应的contextRef并绘图。如果在其他方法中获取将获取到一个invalidate的ref并且不能用于画图。drawRect：方法不能手动显示调用，必须通过调用setNeedsDisplay 或者 setNeedsDisplayInRect，让系统自动调该方法。

2、若使用calayer绘图，只能在drawInContext: 中（类似于drawRect）绘制，或者在delegate中的相应方法绘制。同样也是调用setNeedDisplay等间接调用以上方法

3、若要实时画图，不能使用gestureRecognizer，只能使用touchbegan等方法来掉用setNeedsDisplay实时刷新屏幕



26.layoutSubviews总结


ios layout机制相关方法

- (CGSize)sizeThatFits:(CGSize)size
- (void)sizeToFit
——————-

- (void)layoutSubviews
- (void)layoutIfNeeded
- (void)setNeedsLayout
——————–

- (void)setNeedsDisplay
- (void)drawRect
layoutSubviews在以下情况下会被调用：

1、init初始化不会触发layoutSubviews

   但是是用initWithFrame 进行初始化时，当rect的值不为CGRectZero时,也会触发

2、addSubview会触发layoutSubviews

3、设置view的Frame会触发layoutSubviews，当然前提是frame的值设置前后发生了变化

4、滚动一个UIScrollView会触发layoutSubviews

5、旋转Screen会触发父UIView上的layoutSubviews事件

6、改变一个UIView大小的时候也会触发父UIView上的layoutSubviews事件

在苹果的官方文档中强调:

      You should override this method only if the autoresizing behaviors of the subviews do not offer the behavior you want.

layoutSubviews, 当我们在某个类的内部调整子视图位置时，需要调用。

反过来的意思就是说：如果你想要在外部设置subviews的位置，就不要重写。

刷新子对象布局

-layoutSubviews方法：这个方法，默认没有做任何事情，需要子类进行重写
-setNeedsLayout方法： 标记为需要重新布局，异步调用layoutIfNeeded刷新布局，不立即刷新，但layoutSubviews一定会被调用
-layoutIfNeeded方法：如果，有需要刷新的标记，立即调用layoutSubviews进行布局（如果没有标记，不会调用layoutSubviews）

如果要立即刷新，要先调用[view setNeedsLayout]，把标记设为需要布局，然后马上调用[view layoutIfNeeded]，实现布局

在视图第一次显示之前，标记总是“需要刷新”的，可以直接调用[view layoutIfNeeded]

重绘

-drawRect:(CGRect)rect方法：重写此方法，执行重绘任务
-setNeedsDisplay方法：标记为需要重绘，异步调用drawRect
-setNeedsDisplayInRect:(CGRect)invalidRect方法：标记为需要局部重绘

sizeToFit会自动调用sizeThatFits方法；

sizeToFit不应该在子类中被重写，应该重写sizeThatFits

sizeThatFits传入的参数是receiver当前的size，返回一个适合的size

sizeToFit可以被手动直接调用

sizeToFit和sizeThatFits方法都没有递归，对subviews也不负责，只负责自己

———————————-

layoutSubviews对subviews重新布局

layoutSubviews方法调用先于drawRect

setNeedsLayout在receiver标上一个需要被重新布局的标记，在系统runloop的下一个周期自动调用layoutSubviews

layoutIfNeeded方法如其名，UIKit会判断该receiver是否需要layout.根据Apple官方文档,layoutIfNeeded方法应该是这样的

layoutIfNeeded遍历的不是superview链，应该是subviews链

drawRect是对receiver的重绘，能获得context

setNeedDisplay在receiver标上一个需要被重新绘图的标记，在下一个draw周期自动重绘，iphone device的刷新频率是60hz，也就是1/60秒后重绘



27.如果继承的是UITableViewController 那么self.view 就是tableView
 
28.
iOS清空NSUserDefaults下的内容

//方法一

NSString*appDomain = [[NSBundle mainBundle] bundleIdentifier];

[[NSUserDefaults standardUserDefaults] removePersistentDomainForName:appDomain];

//方法二

- (void)resetDefaults 

{

NSUserDefaults* defs = [NSUserDefaults standardUserDefaults];

NSDictionary* dict = [defs dictionaryRepresentation];

for(id key in dict) {

[defs removeObjectForKey:key];

}

[defs synchronize];

}





29.解决编译时警告：

Prefix.pch文件中加入  
#import <SystemConfiguration/SystemConfiguration.h>  
#import <MobileCoreServices/MobileCoreServices.h> 


30.限制输入框输入字符

return !(textView.text.length>=32 && range.length==0);

31.尽量减少 继承UITableViewController 和 UICollectionViewController

32.   //去掉导航栏的黑线

    [[UINavigationBar appearance] setBackgroundImage:[[UIImage alloc] init] forBarMetrics:UIBarMetricsDefault];

    [[UINavigationBar appearance] setShadowImage:[[UIImage alloc] init]];





33.iOS资料集锦



http://pan.baidu.com/share/home?uk=809747416&view=share#category/type=0

无限互联



http://pan.baidu.com/share/home?uk=3560277524#category/type=0

传智播客



http://pan.baidu.com/share/home?uk=2282799522&view=share#category/type=0

http://pan.baidu.com/share/home?uk=151726140&third=0#category/type=0

http://pan.baidu.com/share/home?uk=2819102520&third=0#category/type=0

http://pan.baidu.com/share/home?third=1&uk=3829188632&start=20#category/type=0

http://pan.baidu.com/share/home?uk=1178428084&third=0#category/type=0





34. 

ios 播放声音和震动

 使用AudioServicesPlaySystemSound 这个接口来进行声音和震动的播放， 当然需要在工程中加入AudioToolBox.framework



1. 播放震动

     

AudioServicesPlaySystemSound(kSystemSoundID_Vibrate);





2. 播放特定的声音


static SystemSoundID soundIDTest = 0;


NSString * path = [[NSBundle mainBundle] pathForResource:@"test" ofType:@"wav"];

if (path) {

      AudioServicesCreateSystemSoundID( (CFURLRef)[NSURL fileURLWithPath:path], &soundIDTest );

}

    AudioServicesPlaySystemSound( soundIDTest );





35.有两种方法：

一，使用NSString的方法：

NSString* string2 = [string1 stringByAddingPercentEscapesUsingEncoding:NSUTF8StringEncoding];

NSString* string1 = [string2 stringByReplacingPercentEscapesUsingEncoding:NSUTF8StringEncoding];

 

二、使用CFStringRef的方法

sUrl = (NSString *)CFURLCreateStringByAddingPercentEscapes(kCFAllocatorDefault, (CFStringRef)sUrl, nil, nil, kCFStringEncodingUTF8);





36.遍历字符串

在oc中遍历字符串的至少可以使用以下两种方法



（1） 通过查找的方式来(这方式适合所有格式的子符串，推荐使用)

   NSString *newStr =@"abdcdddccdd00大家好哦";

   NSString *temp = nil;

   for(int i =0; i < [newStr length]; i++)  

   {   

       temp = [newStr substringWithRange:NSMakeRange(i, 1)];

       NSLog(@"第%d个字是:%@",i,temp);

   }  

   

(2) 通过遍历字符的方式遍历字符串(只适合不包含中文的字符串)

        

   NSString *newStr = @"abdcdddccdd00";


   for(int i =0; i < [newStr length]; i++)  

   {   


      NSLog(@"第%d个字符是:%@",i, [newStr characterAtIndex:i]);

   }  



37.#pragma mark SDWebImage ====清除缓存============

- (long long) fileSizeAtPath:(NSString*) filePath{

    NSFileManager* manager = [NSFileManager defaultManager];

    if ([manager fileExistsAtPath:filePath]){

        return [[manager attributesOfItemAtPath:filePath error:nil] fileSize];

    }

    return 0;

}

//遍历文件夹获得文件夹大小，返回多少M

- (float ) folderSizeAtPath:(NSString*) folderPath{

    NSFileManager* manager = [NSFileManager defaultManager];

    if (![manager fileExistsAtPath:folderPath]) return 0;

    NSEnumerator *childFilesEnumerator = [[manager subpathsAtPath:folderPath] objectEnumerator];

    NSString* fileName;

    long long folderSize = 0;

    while ((fileName = [childFilesEnumerator nextObject]) != nil){

        NSString* fileAbsolutePath = [folderPath stringByAppendingPathComponent:fileName];

        folderSize += [self fileSizeAtPath:fileAbsolutePath];

    }

    return folderSize/(1024.0*1024.0);

}

//1. 清除缓存第一种

- (void)action

{

    //彻底清除缓存第一种方法

    NSArray *paths = NSSearchPathForDirectoriesInDomains(NSLibraryDirectory, NSUserDomainMask, YES);

    NSString *path = [paths lastObject];

    

    NSString *str = [NSString stringWithFormat:@"你确定要清除%.1fM的缓存", [self folderSizeAtPath:path]];

    [self showmessage:str];

    

}

- (void)alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex{

    if(buttonIndex==1){

//                NSArray *paths = NSSearchPathForDirectoriesInDomains(NSLibraryDirectory, NSUserDomainMask, YES);

//                NSString *path = [paths lastObject];

//                NSArray *files = [[NSFileManager defaultManager] subpathsAtPath:path];

//                for (NSString *p in files) {

//                    NSError *error;

//                    NSString *Path = [path stringByAppendingPathComponent:p];

//                    if ([[NSFileManager defaultManager] fileExistsAtPath:Path]) {

//                        [[NSFileManager defaultManager] removeItemAtPath:Path error:&error];

//                    }

//                }

        

        //  2. SDImage第三方清除缓存的方法

//        [[SDImageCache sharedImageCache] cleanDisk];

//        [[SDImageCache sharedImageCache] clearMemory];

        

           //3. 彻底清除缓存第二种方法

                dispatch_async(

                               dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0)

                               , ^{

                                   NSString *cachPath = [NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES) objectAtIndex:0];

                                   NSLog(@"%@", cachPath);

        

                                   NSArray *files = [[NSFileManager defaultManager] subpathsAtPath:cachPath];

                                   NSLog(@"files :%ld",[files count]);

                                   for (NSString *p in files) {

                                       NSError *error;

                                       NSString *path = [cachPath stringByAppendingPathComponent:p];

                                       if ([[NSFileManager defaultManager] fileExistsAtPath:path]) {

                                           [[NSFileManager defaultManager] removeItemAtPath:path error:&error];

                                       }

                                   }

                                   [self performSelectorOnMainThread:@selector(clearCacheSuccess) withObject:nil waitUntilDone:YES];});

    }else{

    }

}



-(void)showmessage:(NSString*)message

{

    UIAlertView *al = [[UIAlertView alloc]initWithTitle:@"提示" message:message delegate:self cancelButtonTitle:@"取消" otherButtonTitles:@"确定", nil];

    [al show];

}

-(void)clearCacheSuccess

{

    [self showHint:@"清理成功"];

}



37.复制链接

  UIPasteboard *pab = [UIPasteboard generalPasteboard];
        
        NSString *string = @"测试";
        
        [pab setString:string];
        
        if (pab == nil) {
            [MBProgressHUD showError:@"复制失败"];
            
        }else
        {
            [MBProgressHUD showSuccess:@"已复制"];
        } 

38.显示/隐藏Mac隐藏文件命令如下(注意其中的空格并且区分大小写)：

显示Mac隐藏文件的命令：defaults write com.apple.finder AppleShowAllFiles -bool true
隐藏Mac隐藏文件的命令：defaults write com.apple.finder AppleShowAllFiles -bool false
或者
显示Mac隐藏文件的命令：defaults write com.apple.finder AppleShowAllFiles YES
隐藏Mac隐藏文件的命令：defaults write com.apple.finder AppleShowAllFiles NO
输完单击Enter键，退出终端，重新启动Finder就可以了
注意：1、执行命令后需要重启 Finder 才能看到效果。 　　　　
        　2、不要乱动不懂的隐藏文件，可能会损坏你的系统。
重启Finder：鼠标单击窗口左上角的苹果标志-->强制退出—>Finde

39.iOS如何把所有界面的状态栏的字体颜色都设置为白色
第一步：在info.plist中添加一个字段：view controller -base status bar 设置为NO



第二步：在一个所有界面都继承的父类里添加：

  if (IOS7_OR_LATER) { // 判断是否是IOS7

    [[UIApplication sharedApplication] setStatusBarStyle:UIStatusBarStyleLightContent animated:NO];

  }



40

一句话解决所有TableView的多余cell【原创】

就一句代码放在AppDelegate里，其他的不多说了

1
[[UITableView appearance] setTableFooterView:[UIView new]];



```

## 公司
```objc

学号：               1110402006
姓名：               何千元
专业：               电子信息科学与技术
就业单位：         深圳市诺贝儿教育投资发展有限公司
个人联系方式：   186-7464-0795
单位联系电话：    0755 - 26409988
单位传真       :     0755 - 26403388
单位邮箱       :     lif@sznobel.com
单位地址       :     深圳市南山区科技园科技南十二路康佳研发大赛8G-H
单位网址       :     www.sznobel.com

```


## 工具
* Mark Man
* Foxmail
* Axure RP Pro 7.0
* iZip UnArchiver
* GitHub DeskTop
* 今目标
* CornerStone
* licecap
* Mou
* PicGIF Lite
* GitBook Edit
* Iterm
* Mindjet MindManager
* 

## 第三方
* 百度地图
* 百度统计
* 个推
* 环信
* 极光
* 讯飞语音
* 友盟
* ShareSDK


## GitHubResource

IOSDevelopNet：
**1.资源网站
http://code4app.com/
http://www.cocoachina.com/
http://www.oschina.net/
http://www.codeios.com/


* 1. iOS1000个常用库
http://www.open-open.com/lib/view/open1433383487729.html
* 2.ios 常用的加密解密
http://www.th7.cn/Program/Android/201504/441779.shtml
* 3.ios控制器容器
* http://www.tuicool.com/articles/3ymMzub
* 4.适配iOS9
* http://www.cnblogs.com/jukaiit/p/5015889.html?utm_source=tuicool&utm_medium=referral
* http://www.tuicool.com/articles/7bY3my
* 5.应用托管平台<https://fir.im/>
* 6.AppIcon 和 Luanch Image大小
* http://blog.csdn.net/yqmfly/article/details/43525397


* <https://github.com/zeqinjie/AddressChoicePickViewDemo>
* <https://github.com/AFNetworking/AFNetworking>
* <https://github.com/ArtFeel/AFViewShaker>
* <https://github.com/alcatraz/Alcatraz>
* <https://github.com/lobianco/ALMoviePlayerController>
* <https://github.com/andreamazz/AMPopTip>
* <https://github.com/andreamazz/AMScrollingNavbar>
* <https://github.com/andreamazz/AMWaveTransition>
* <https://github.com/onevcat/APNGKit>
* <https://github.com/autresphere/ASMediaFocusManager>
* <https://github.com/alskipp/ASProgressPopUpView>
* <https://github.com/facebook/AsyncDisplayKit>
* <https://github.com/Awhisper/AsyncDisplayKitDocTranslation>
* <https://github.com/mzds/AVPlayerDemo>
* <https://github.com/levey/AwesomeMenu>
* <https://github.com/coolnameismy/BabyBluetooth>
* <https://github.com/antiguab/BAFluidView>
* <https://github.com/nicklockwood/Base64>
* <https://github.com/TanguyAladenise/BBBadgeBarButtonItem>
* <https://github.com/chenxiaoyu3/BBStockChartView>
* <https://github.com/Boris-Em/BEMSimpleLineGraph>
* <https://github.com/gpambrozio/BlockAlertsAnd-ActionSheets>
* <https://github.com/lizelu/CATransitionDemo>
* <https://github.com/CharlinFeng/CFCityPickerVC>
* <https://github.com/zhiyu/chartee>
* <https://github.com/danielgindi/Charts>
* <https://github.com/dormitory219/ChatKit>
* <https://github.com/chiahsien/CHTCollectionViewWaterfallLayout>
* <https://github.com/chrismiles/CMPopTipView>
* <https://github.com/limccn/Cocoa-Charts>
* <https://github.com/CocoaLumberjack/CocoaLumberjack>
* <https://github.com/kelp404/CocoaSecurity>
* <https://github.com/omz/ColorSense-for-Xcode>
* <https://github.com/bennyguitar/Colours>
* <https://github.com/core-plot/core-plot>
* <https://github.com/CharlinFeng/CoreArchive>
* <https://github.com/CharlinFeng/CoreFMDB>
* <https://github.com/CharlinFeng/CoreJPush>
* <https://github.com/CharlinFeng/CoreLock>
* <https://github.com/CharlinFeng/CoreMediaFuncManagerVC>
* <https://github.com/CharlinFeng/CoreModel>
* <https://github.com/CharlinFeng/CorePhotoBroswerVC>
* <https://github.com/CharlinFeng/CoreTFManagerVC>
* <https://github.com/CharlinFeng/CoreUmeng>
* <https://github.com/CSStickyHeaderFlowLayout/CSStickyHeaderFlowLayout>
* <https://github.com/chiunam/CTAssetsPickerController>
* <https://github.com/Mydly/CustomLabel>
* <https://github.com/ChenYilong/CYLTabBarController>
* <https://github.com/danielamitay/DACircularProgress>
* <https://github.com/donobono/DoImagePickerController>
* <https://github.com/12207480/DOPDropDownMenu-Enhanced>
* <https://github.com/oarrabi/Download-Manager>
* <https://github.com/CoderJackyHuang/DownloadManager>
* <https://github.com/sam408130/DSLolita>
* <https://github.com/xiekw2010/DXAlertView>
* <https://github.com/dzenbot/DZNEmptyDataSet>
* <https://github.com/dzenbot/DZNPhotoPickerController>
* <https://github.com/dzenbot/DZNSegmentedControl>
* <https://github.com/easemob/easeui_ios>
* <https://github.com/EnjoySR/ESJsonFormat-Xcode>
* <https://github.com/WilliamZang/FastAnimationWithPOP>
* <https://github.com/Seitk/FB-Gallery>
* <https://github.com/forkingdog/FDFullscreenPopGesture>
* <https://github.com/FFmpeg/FFmpeg>
* <https://github.com/iMoreApps/ffmpeg-avplayer-for-ios-tvos>
* <https://github.com/ccgus/fmdb>
* <https://github.com/tangqiaoboy/FmdbSample>
* <https://github.com/nicklockwood/FXBlurView>
* <https://github.com/nicklockwood/FXForms>
* <https://github.com/GitbookIO/gitbook>
* <https://github.com/BradLarson/GPUImage>
* <https://github.com/gsdios/GSD_WeiXin>
* <https://github.com/r258833095/GTMBase64>
* <https://github.com/ArtSabintsev/Harpy>
* <https://github.com/hsousa/HCSStarRatingView>
* <https://github.com/topfunky/hpple>
* <https://github.com/Heikowi/HWIFileDownload>
* <https://github.com/CoderJackyHuang/HYBLoopScrollView>
* <https://github.com/CoderJackyHuang/HYBNetworking>
* <https://github.com/huzhiqin/HZQDatePickerView>
* <https://github.com/iltercengiz/ICViewPager>
* <https://github.com/w3sy/ImagesScrollView>
* <https://github.com/lzyy/iOS-Developer-Interview-Questions>
* <https://github.com/moqod/ios-qr-code-encoder>
* <https://github.com/ios122/ios122>
* <https://github.com/shinobicontrols/iOS7-day-by-day>
* <https://github.com/ChenYilong/iOS9AdaptationTips>
* <https://github.com/yixiangboy/IOSAnimationDemo>
* <https://github.com/tangqiaoboy/iOSBlogCN>
* <https://github.com/ChenYilong/iOSInterviewQuestions>
* <https://github.com/hackiftekhar/IQKeyboardManager>
* <https://github.com/nicklockwood/iRate>
* <https://github.com/Jawbone/JBChartView>
* <https://github.com/johnil/JFImagePickerController>
* <https://github.com/JonasGessner/JGProgressHUD>
* <https://github.com/jhurray/JHChainableAnimations>
* <https://github.com/Jinxiansen/JHUD>
* <https://github.com/shaojiankui/JKCategories>
* <https://github.com/shaojiankui/JKSideSlipView>
* <https://github.com/jimneylee/JLSinaMBlogNimbus>
* <https://github.com/JaviSoto/JSBadgeView>
* <https://github.com/johnezang/JSONKit>
* <https://github.com/jsonmodel/jsonmodel>
* <https://github.com/jessesquires/JSQMessagesViewController>
* <https://github.com/Jiar/KeyboardToolBar>
* <https://github.com/kishikawakatsumi/KeychainAccess>
* <https://github.com/36Kr-Mobile/KRVideoPlayer>
* <https://github.com/ksuther/KSImageNamed-Xcode>
* <https://github.com/mikeMTOL/KSVideoPlayer>
* <https://github.com/kolyvan/kxmenu>
* <https://github.com/kolyvan/kxmovie>
* <https://github.com/kolyvan/kxtorrent>
* <https://github.com/lukabernardi/LBBlurredImage>
* <https://github.com/MxABC/LBXScan>
* <https://github.com/nonstriater/Learn-Algorithms>
* <https://github.com/shiqiang124/LFRoundProgressView>
* <https://github.com/runner365/LiveVideoCoreSDK>
* <https://github.com/li6185377/LKDBHelper-SQLite-ORM>
* <https://github.com/lsmakethebest/LSPlayer>
* <https://github.com/JustKeepRunning/LXDScanQRCode>
* <https://github.com/Marxon13/M13ProgressSuite>
* <https://github.com/AlexandrGraschenkov/MagicPie>
* <https://github.com/guoyunsky/Markdown-Chinese-Demo>
* <https://github.com/SnapKit/Masonry>
* <https://github.com/XQBoy/MasonryExercise>
* <https://github.com/jdg/MBProgressHUD>
* <https://github.com/poholo/MCPayDemo>
* <https://github.com/xhzengAIB/MessageDisplayKit>
* <https://github.com/matteogobbi/MGSpotyViewController>
* <https://github.com/MortimerGoro/MGSwipeTableCell>
* <https://github.com/CoderMJLee/MJDownload>
* <https://github.com/CoderMJLee/MJExtension>
* <https://github.com/martinjuhasz/MJPopupViewController>
* <https://github.com/CoderMJLee/MJRefresh>
* <https://github.com/MugunthKumar/MKNetworkKit>
* <https://github.com/MakeZL/ZLPhotoLib>
* <https://github.com/mutualmobile/MMDrawerController>
* <https://github.com/mgcm/MMPopLabel>
* <https://github.com/mutualmobile/MMProgressHUD>
* <https://github.com/mownier/MONActivityIndicatorView>
* <https://github.com/zhengjinghua/MQRCodeReaderViewController>
* <https://github.com/mrackwitz/MRProgress>
* <https://github.com/erichoracek/MSDynamicsDrawerViewController>
* <https://github.com/MartinRGB/MTMaterialDelete>
* <https://github.com/mwaterfall/MWPhotoBrowser>
* <https://github.com/youngsoft/MyLinearLayout>
* <https://github.com/NachoSoto/NSBKeyframeAnimation>
* <https://github.com/Nyx0uf/NYXImagesKit>
* <https://github.com/bendytree/Objective-C-RegEx-Categories>
* <https://github.com/dkhamsing/open-source-ios-apps>
* <https://github.com/Vinodh-G/ParallaxTableViewHeader>
* <https://github.com/kondratyevdev/Path-Intro-iPhone>
* <https://github.com/ioswpf/PayDemo>
* <https://github.com/piemonte/PBJVideoPlayer>
* <https://github.com/piemonte/PBJVision>
* <https://github.com/kishikawakatsumi/PEPhotoCropEditor>
* <https://github.com/iThinkerYZ/PersonalFramework>
* <https://github.com/CharlinFeng/PhotoBrowser>
* <https://github.com/kimziv/PinYin4Objc>
* <https://github.com/kevinzhow/PNChart>
* <https://github.com/facebook/pop>
* <https://github.com/schneiderandre/popping>
* <https://github.com/MartinLi841538513/ProduceQRCodeDemo>
* <https://github.com/ptshih/PSCollectionView>
* <https://github.com/slipawayleaon/PSDrawerManager>
* <https://github.com/steipete/PSStackedView>
* <https://github.com/steipete/PSTAlertController>
* <https://github.com/steipete/PSTCollectionView>
* <https://github.com/questbeat/QBImagePicker>
* <https://github.com/HarrisLee/QBImagePickerController>
* <https://github.com/questbeat/QBPopupMenu>
* <https://github.com/quemb/QMBParallaxScrollViewController>
* <https://github.com/dongxiexidu/QR-Code>
* <https://github.com/WuKongCoo1/QRCodeReader>
* <https://github.com/yannickl/QRCodeReaderViewController>
* <https://github.com/Augustyniak/RATreeView>
* <https://github.com/tonymillion/Reachability>
* <https://github.com/ReactiveCocoa/ReactiveCocoa>
* <https://github.com/romaonthego/REFrostedViewController>
* <https://github.com/wezm/RegexKitLite>
* <https://github.com/romaonthego/RESideMenu>
* <https://github.com/RestKit/RestKit>
* <https://github.com/romaonthego/RETableViewManager>
* <https://github.com/cwRichardKim/RKDropdownAlert>
* <https://github.com/cwRichardKim/RKNotificationHub>
* <https://github.com/cwRichardKim/RKSwipeBetweenViewControllers>
* <https://github.com/ruslanskorb/RSKImageCropper>
* <https://github.com/rickytan/RTImageAssets>
* <https://github.com/honcheng/RTLabel>
* <https://github.com/soffes/SAMKeychain>
* <https://github.com/strivingboy/scan_qrcode_demo>
* <https://github.com/rFlex/SCViewShaker>
* <https://github.com/gsdios/SDAutoLayout>
* <https://github.com/gsdios/SDCycleScrollView>
* <https://github.com/easemob/sdkdemoapp3.0_ios>
* <https://github.com/rs/SDWebImage>
* <https://github.com/li6185377/SDWebImage-Category>
* <https://github.com/kevinrenskers/SDWebImage-ProgressView>
* <https://github.com/MobClub/ShareSDK-for-iOS>
* <https://github.com/Sumi-Interactive/SIAlertView>
* <https://github.com/siqin/SimpleCalendar>
* <https://github.com/khanlou/SKBounceAnimation>
* <https://github.com/Spaceman-Labs/SMPageControl>
* <https://github.com/soffes/sstoolkit>
* <https://github.com/zhengjinghua/StitchingImage>
* <https://github.com/dangfm/stockChart>
* <https://github.com/STShenZhaoliang/STPhotoBrowser>
* <https://github.com/SVProgressHUD/SVProgressHUD>
* <https://github.com/TransitApp/SVWebViewController>
* <https://github.com/CharlinFeng/SwipeNavigationVC>
* <https://github.com/nicklockwood/SwipeView>
* <https://github.com/dsxNiubility/SXNews>
* <https://github.com/TanguyAladenise/TAPageControl>
* <https://github.com/suifengqjn/TBPlayer>
* <https://github.com/mogujie/TeamTalk>
* <https://github.com/tLewisII/TLAlertView>
* <https://github.com/TimOliver/TOCropViewController>
* <https://github.com/michaeltyson/TPKeyboardAvoiding>
* <https://github.com/TinyQ/TQStarRatingView>
* <https://github.com/yixiangboy/TreeTableView>
* <https://github.com/TTTAttributedLabel/TTTAttributedLabel>
* <https://github.com/toniomg/TutorialBase>
* <https://github.com/chasseurmic/TWRDownloadManager>
* <https://github.com/12207480/TYDownloadManager>
* <https://github.com/JJSaccolo/UIActivityIndicator-for-SDWebImage>
* <https://github.com/jivadevoe/UIAlertView-Blocks>
* <https://github.com/kishikawakatsumi/UICKeyChainStore>
* <https://github.com/mokagio/UICollectionViewLeftAlignedLayout>
* <https://github.com/AliSoftware/UIImage-Resize>
* <https://github.com/coryalder/UIImage_Resize>
* <https://github.com/yfme/UIImageView-PlayGIF>
* <https://github.com/mxcl/UIImageWithColor>
* <https://github.com/huang303513/UILayoutOfiOS>
* <https://github.com/forkingdog/UITableView-FDTemplateLayoutCell>
* <https://github.com/andreamazz/UITextField-Shake>
* <https://github.com/andreamazz/UIView-Shake>
* <https://github.com/u10int/URBAlertView>
* <https://github.com/blizzard-op/VideoPlayerKit>
* <https://github.com/viki-org/VKVideoPlayer>
* <https://github.com/onevcat/VVDocumenter-Xcode>
* <https://github.com/johnil/VVeboTableViewDemo>
* <https://github.com/wokalski/WCActionSheet>
* <https://github.com/xiaoliguang/WechatPayDemo>
* <https://github.com/zhengwenming/WMPlayer>
* <https://github.com/renzifeng/WXPay>
* <https://github.com/leichunfeng/WXTabBarController>
* <https://github.com/nicolaschengdev/WYPopoverController>
* <https://github.com/qfish/XAlign>
* <https://github.com/0xced/XCDYouTubeKit>
* <https://github.com/JackTeam/XHImageViewer>
* <https://github.com/HebeTienCoder/XLPlainFlowLayout>
* <https://github.com/wazrx/XWEasyKVONotification>
* <https://github.com/android1989/YetiCharacterLabelExample>
* <https://github.com/yuantiku/YTKNetwork>
* <https://github.com/ibireme/YYCache>
* <https://github.com/dcty/YYJSON>
* <https://github.com/ibireme/YYKit>
* <https://github.com/ibireme/YYModel>
* <https://github.com/ibireme/YYText>
* <https://github.com/ibireme/YYWebImage>
* <https://github.com/iThinkerYZ/YZDisplayViewController>
* <https://github.com/renzifeng/ZFDownload>
* <https://github.com/renzifeng/ZFPlayer>
* <https://github.com/MakeZL/ZLPhotoLib>
* <https://github.com/heroims/ZYQAssetPickerController>
* 


