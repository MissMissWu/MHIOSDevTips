# Block

---
## 开篇扯淡

* As a local variable:    <br>

```objc
returnType (^blockName)(parameterTypes) = ^returnType(parameters) {...};
```
* As a property:    <br>

```objc
@property (nonatomic, copy, nullability) returnType (^blockName)(parameterTypes);
```
* As a method parameter: <br>

```objc
- (void)someMethodThatTakesABlock:(returnType (^nullability)(parameterTypes))blockName;
```
* As an argument to a method call: <br>

```objc
[someObject someMethodThatTakesABlock:^returnType (parameters) {...}];
```

* As a typedef:  <br>

```objc
typedef returnType (^TypeName)(parameterTypes);
TypeName blockName = ^returnType(parameters) {...};
```

## 参考链接

* [如何声明一个代码快 block](http://fuckingblocksyntax.com/)