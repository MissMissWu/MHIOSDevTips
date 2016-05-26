# UIGestureRecognizer

### UIGestureRecognizer

UIGestureRecognizer基类是一个抽象类,我们只能使用它的拓展类。
* UIGestureRecognizer类的扩展类   
  * `UITapGestureRecognizer` 
  * `UIPinchGestureRecognizer `
  * `UIRotationGestureRecognizer` 
  * `UISwipeGestureRecognizer `
  * `UIPanGestureRecognizer `
  * `UILongPressGestureRecognizer`  
  
*UIGestureRecognizer知识点
  * 一个gesture recognizer是针对一个特定的view的（包含其subview），用UIView的方法addGestureRecognize：去关联一个view
  * 一个gesture recognizer是不参与UIView的事件响应链的
  * 手势识别是具有互斥的原则的
  * **[A requireGestureRecognizerToFail：B]** 函数，它可以指定当A手势发生时，即便A已经滿足条件了，也不会立刻触发，会等到指定的手势B确定失败之后才触发。

* 参考链接
  * <http://blog.csdn.net/namehzf/article/details/7424882>
  * <http://www.2cto.com/kf/201504/395305.html>
  * <http://blog.csdn.net/majiakun1/article/details/17333683>