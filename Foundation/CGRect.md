# CGRect
---
* CGRectInset  
``` objc
CGRect CGRectInset (
   CGRect rect,
   CGFloat dx,
   CGFloat dy
);
```  
**说明:** 该结构体的应用是以原rect为中心，再参考dx，dy，进行缩放或者放大。

![CGRectInset](http://images.cnblogs.com/cnblogs_com/85538649/CGRectInset.jpg)

**说明:** 图中的每一个矩形都是以上一个矩形作为参考矩形。所以下一矩形（比如黄色矩形对绿色矩形来说是下一个矩形）都比上一个矩形要小。  
具体小多少都是要参照dx和dy来判定的。<br />

---

* CGRectOffset  
```objc
CGRect CGRectOffset(
    CGRect rect,
    CGFloat dx,
    CGFloat dy
);
```   
** 说明 ：**相对于源矩形原点rect（左上角的点）沿x轴和y轴偏移, 再rect基础上沿x轴和y轴偏移


---


* frame和dounds  
frame和bounds是UIView中的两个属性(property)。  
``` objc
-(CGRect)frame
{
    return CGRectMake(self.frame.origin.x,self.frame.origin.y,self.frame.size.width,self.frame.size.height);
}
-(CGRect)bounds
{
    return CGRectMake(0,0,self.frame.size.width,self.frame.size.height);
}
```

  * frame指的是：该view在父view坐标系统中的位置和大小。（参照点是父亲的坐标系统）
  * bounds指的是：该view在本身坐标系统中 的位置和大小。（参照点是本身坐标系统） <br />    
  
  ![frameAndBounds](http://pic002.cnblogs.com/images/2011/315766/2011081514215034.png)

