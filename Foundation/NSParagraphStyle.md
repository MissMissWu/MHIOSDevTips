# NSParagraphStyle
## 开篇扯淡
- 主要是介绍富文本段落的设置属性, 主要使用可变的段落设置 `NSMutableParagraphStyle`

## 属性介绍
```objc
typedef NS_ENUM(NSInteger, NSLineBreakMode) {/* What to do with long lines */
    NSLineBreakByWordWrapping = 0,     /* Wrap at word boundaries, default */
    NSLineBreakByCharWrapping,/* Wrap at character boundaries */
    NSLineBreakByClipping,/* Simply clip */剪掉后面显示不了的部分
    NSLineBreakByTruncatingHead,/* Truncate at head of line: "...wxyz" */头部分的内容以……方式省略
    NSLineBreakByTruncatingTail,/* Truncate at tail of line: "abcd..." */结尾部分的内容以……方式省略
    NSLineBreakByTruncatingMiddle/* Truncate middle of line:  "ab...yz" */中间部分的内容以……方式省略
} NS_ENUM_AVAILABLE_IOS(6_0);


typedef NS_ENUM(NSInteger, NSWritingDirection) {
    NSWritingDirectionNatural       = -1,    // Determines direction using the Unicode Bidi Algorithm rules P2 and P3
    NSWritingDirectionLeftToRight   =  0,    // Left to right writing direction 左到右的书写方向
    NSWritingDirectionRightToLeft   =  1    // Right to left writing direction 右到左的书写方向
} NS_ENUM_AVAILABLE_IOS(6_0);


 //   NSParagraphStyleAttributeName 段落的风格（设置首行，行间距，对齐方式什么的）看自己需要什么属性，写什么
    NSMutableParagraphStyle *paragraphStyle = [[NSMutableParagraphStyle alloc] init];
    paragraphStyle.lineSpacing = 10;// 字体的行间距
    paragraphStyle.firstLineHeadIndent = 20.0f;//首行缩进
    paragraphStyle.alignment = NSTextAlignmentJustified;//（两端对齐的）文本对齐方式：（左，中，右，两端对齐，自然）
    paragraphStyle.lineBreakMode = NSLineBreakByTruncatingTail;//结尾部分的内容以……方式省略 ( "...wxyz" ,"abcd..." ,"ab...yz")
    paragraphStyle.headIndent = 20;//整体缩进(首行除外)
    paragraphStyle.tailIndent = 20;//
    paragraphStyle.minimumLineHeight = 10;//最低行高
    paragraphStyle.maximumLineHeight = 20;//最大行高
    paragraphStyle.paragraphSpacing = 15;//段与段之间的间距
    paragraphStyle.paragraphSpacingBefore = 22.0f;//段首行空白空间/* Distance between the bottom of the previous paragraph (or the end of its paragraphSpacing, if any) and the top of this paragraph. */
    paragraphStyle.baseWritingDirection = NSWritingDirectionLeftToRight;//从左到右的书写方向（一共➡️三种）
    paragraphStyle.lineHeightMultiple = 15;/* Natural line height is multiplied by this factor (if positive) before being constrained by minimum and maximum line height. */
    paragraphStyle.hyphenationFactor = 1;//连字属性 在iOS，唯一支持的值分别为0和1







/*
  NSFontAttributeName 字体大小
  NSParagraphStyleAttributeName 段落的风格（设置首行，行间距，对齐方式什么的）
  NSKernAttributeName 字间距
 */
    NSDictionary *attributes = @{
                                 NSFontAttributeName:[UIFont systemFontOfSize:15],
                                 NSParagraphStyleAttributeName:paragraphStyle,
                                 NSKernAttributeName:@(10),
                                                              
                                 };
    textView.attributedText = [[NSAttributedString alloc] initWithString:textView.text attributes:attributes];

```

## 参考链接
* <http://blog.csdn.net/u010241322/article/details/40894069>
* 