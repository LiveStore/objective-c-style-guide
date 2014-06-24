objective-c-style-guide
=======================

以下为 时尚Cosmo 团队所执行 Objective-C 编码规范。


## 介绍

下面是一些从苹果公司所提供的编码规范。如果在开发过程中某些细节此文档没给出示范，请在苹果编码规范中寻找

* [The Objective-C Programming Language](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/ObjectiveC/Introduction/introObjectiveC.html)
* [Cocoa Fundamentals Guide](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CocoaFundamentals/Introduction/Introduction.html)
* [Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
* [iOS App Programming Guide](http://developer.apple.com/library/ios/#documentation/iphone/conceptual/iphoneosprogrammingguide/Introduction/Introduction.html)

## 格式

### 空格替换制表符

使用空格缩进。不要在代码中使用制表符。你应该将编辑器设置成自动将制表符替换成空格。

- 每次缩进4个空格

### 间距

二元运算符和参数之间需要放置一个空格，一元运算符、强制类型转换和参数之间不需要空格。关键字之后圆括号之前需要放置一个空格。

```objc
for (int i = 0; i < 10; i++) {
    int a = (float)b;    
}
```

### 行宽

建议：每一行代码不要超过100个字符。每一个方法前都有一个99字符宽的注释行

```objc
///////////////////////////////////////////////////////////////////////////////////////////////////
- (void)someMethod
{
    //Do something important;
}
```

### 条件语句(`if`\`else`\`switch`)

**推荐:**
```objc
if (user.isHappy) {
	//Do something
}
else {
	//Do something else
}
```

**不推荐:**
```objc
if (user.isHappy)
{
	//Do something
}
else
{
	//Do something else
}
```

能用switch尽量使用switch替代if

- `case` 要缩进
- `case` 与 `default` 对齐
- 每个 `case` 中的代码都要写在 `{}` 中
- `break` 不要写在 `{}` 外

```objc
switch (xxx) {
    case AAA: {
        // do something...
        break;
    }
    default: {
        // do something...
        break;
    }
}
```

### 方法声明和定义

### 方法调用

### @public 和 @private

### 协议名

### block

## 命名

### 文件名
### 类名
### 类别名
### Objective-C 方法名
### 变量名
普通变量名
实例变量
常量


## 注释
文件注释
	版权信息及维护人

声明部分的注释
实现部分的注释





## 参考内容
- [Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html#//apple_ref/doc/uid/10000146-SW1)
- [The official raywenderlich.com Objective-C style guide.](https://github.com/raywenderlich/objective-c-style-guide)
- [NYTimes Objective-C Style Guide](https://github.com/NYTimes/objective-c-style-guide)
- [Coding Guidelines for Cocoa (Github)](https://github.com/github/objective-c-conventions)
- [Google Objective-C Style Guide](http://google-styleguide.googlecode.com/svn/trunk/objcguide.xml)
- [Google 开源项目风格指南](http://zh-google-styleguide.readthedocs.org/en/latest/google-objc-styleguide/contents/)
- [编写高质量的Objective-C代码](http://www.cnblogs.com/xdream86/p/3309345.html)
