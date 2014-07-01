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
    ...
}
```

### 条件语句(`if` \ `else` \ `switch`)

**推荐:**
```objc
if (user.isHappy) {
    ...
}
else {
    ...
}
```

**不推荐:**
```objc
if (user.isHappy)
{
    ...
}
else
{
    ...
}
```

所有的逻辑块必须使用 `{}` 包围，即使条件体只需编写一行代码也必须使用花括号。

**推荐:**

```objc
if (!error) {
    return success;
}
```

**严令禁止:**

```objc
if (!error)
    return success;
```
或：

```objc
if (!error) return success;
```

能用switch尽量使用switch替代if

- `case` 要缩进
- `case` 与 `default` 对齐
- 每个 `case` 中的代码都要写在 `{}` 中
- `break` 不要写在 `{}` 外

```objc
switch (user.gender) {
    case MALE: {
        ...
        break;
    }
    case FEMALE: {
        ...
        break;
    }
    default: {
        ...
        break;
    }
}
```

### 三元运算符

三元运算符要有 `()` 包裹，且括号与语句间不能有空格，`?` 与 `:` 左右要有一个空格
```
label.title = (title ? title : @"");
```


### 方法声明和定义

- `+` 和返回类型之间须使用一个空格，参数列表中只有参数之间可以有空格。
- `{` 要另起一行。

方法应该像这样：

```objc
- (void)doSomethingWithString:(NSString *)theString
{
    ...
}
```

星号前的空格是可选的。当写新的代码时，要与先前代码保持一致。

如果一行有非常多的参数，更好的方式是将每个参数单独拆成一行。如果使用多行，将每个参数前的冒号对齐。

```objc
- (void)doSomethingWith:(GTMFoo *)theFoo
                   rect:(NSRect)theRect
               interval:(float)theInterval
{
    ...
}
```

当第一个关键字比其它的短时，保证下一行至少有 4 个空格的缩进。这样可以使关键字垂直对齐，而不是使用冒号对齐：

```objc
- (void)short:(GTMFoo *)theFoo
    longKeyword:(NSRect)theRect
    evenLongerKeyword:(float)theInterval
{
    ...
}
```

### 方法调用

方法调用应尽量保持与方法声明的格式一致。当格式的风格有多种选择时，新的代码要与已有代码保持一致。

调用时所有参数应该在同一行：

```objc
[myObject doFooWith:arg1 name:arg2 error:arg3];
```

或者每行一个参数，以冒号对齐：

```objc
[myObject doFooWith:arg1
               name:arg2
              error:arg3];
```

不要使用下面的缩进风格：

```objc
[myObject doFooWith:arg1 name:arg2 // some lines with >1 arg
              error:arg3];

[myObject doFooWith:arg1
               name:arg2 error:arg3];

[myObject doFooWith:arg1
          name:arg2 // aligning keywords instead of colons
          error:arg3];
```

方法定义与方法声明一样，当关键字的长度不足以以冒号对齐时，下一行都要以四个空格进行缩进。

```objc
[myObj short:arg1
    longKeyword:arg2
    evenLongerKeyword:arg3];
```

### @public 和 @private

- `@public` 和 `@private` 访问修饰符应该以 `2` 个空格缩进。

```objc
@interface MyClass : NSObject
{
  @public
    ...
  @private
    ...
}
@end
```

### 协议名

由于代理方法的声明一般都很长，所以必须将代理对象和其他的协议对象放在实例变量定义的下面，否则实例变量定义的对齐方式将会被打乱掉。

当需要实现多个协议的时候，将每一个协议名拆分到单独的行。

**推荐:**

```objc
@interface CustomModelViewController : TTViewController
<
  TTModelDelegate,
  TTURLRequestDelegate
>
{
    ...
}
```

### block

`block` 适合用在 target/selector 模式下创建回调方法时，因为它使代码更易读。块中的代码应该缩进 `4` 个空格。
取决于块的长度，下列都是合理的风格准则：

- 如果一行可以写完块，则没必要换行。
- 如果不得不换行，关括号应与块声明的第一个字符对齐。
- 块内的代码须按 `4` 空格缩进。
- 如果块太长，比如超过 `20` 行，建议把它定义成一个局部变量，然后再使用该变量。
- 如果块不带参数，`^{` 之间无须空格。如果带有参数，`^(` 之间无须空格，但 `) {` 之间须有一个空格。

```objc
// The entire block fits on one line.
[operation setCompletionBlock:^{ [self onOperationDone]; }];

// The block can be put on a new line, indented four spaces, with the
// closing brace aligned with the first character of the line on which
// block was declared.
[operation setCompletionBlock:^{
    [self.delegate newDataAvailable];
}];

// Using a block with a C API follows the same alignment and spacing
// rules as with Objective-C.
dispatch_async(fileIOQueue_, ^{
    NSString *path = [self sessionFilePath];
    if (path) {
        ...
    }
});

// An example where the parameter wraps and the block declaration fits
// on the same line. Note the spacing of |^(SessionWindow *window) {|
// compared to |^{| above.
[[SessionService sharedService]
    loadWindowWithCompletionBlock:^(SessionWindow *window) {
        if (window) {
            [self windowDidLoad:window];
        }
        else {
            [self errorLoadingWindow];
        }
    }
];

// An example where the parameter wraps and the block declaration does
// not fit on the same line as the name.
[[SessionService sharedService]
    loadWindowWithCompletionBlock:
        ^(SessionWindow *window) {
            if (window) {
                [self windowDidLoad:window];
            }
            else {
                [self errorLoadingWindow];
            }
        }
];

// Large blocks can be declared out-of-line.
void (^largeBlock)(void) = ^{
    ...
};
[operationQueue_ addOperationWithBlock:largeBlock];
```

## 命名

### 类名

类名（以及类别、协议名）应有 `COS` 前缀，并以驼峰格式分割单词。

例如：`COSViewController`、`COSTableViewCell`。

### 类别名（Category）

类别名应该有 `COS` 前缀以表示类别是项目的一部分或者该类别是通用的。类别名应该包含它所扩展的类的名字。

比如我们要基于 NSString 创建一个用于解析的类别，我们将把类别放在一个名为 `COSNSString+Parsing.h` 的文件中。类别本身命名为 COSStringParsingAdditions （是的，我们知道类别名和文件名不一样，但是这个文件中可能存在多个不同的与解析有关类别）。类别中的方法应该以 cos_myCategoryMethodOnAString: 为前缀以避免命名冲突，因为 Objective-C 只有一个名字空间。如果代码不会分享出去，也不会运行在不同的地址空间中，方法名字就不那么重要了。

类名与包含类别名的括号之间，应该以一个空格分隔。

- 引入第三方实现的 Category 不用遵守此规范。

### Objective-C 方法名

- 方法名应该以小写字母开头，并混合驼峰格式。
- 方法名不要使用 `new` 作为前缀。

一个方法的命名首先描述返回什么，接着是什么情况下被返回。

**参考:**

```objc
emails = [mailbox messagesReceivedAfterDate:yesterdayDate]; // thing + condition + type
```

### Objective-C 方法参数名

- 每个具名参数也应该以小写字母开头，一般使用前缀包括 `a`、`the`、`an` 等。

**参考:**

```objc
- (void)setTitl:(NSString *)aTitle;
```

### 变量名

变量的命名应尽量做到自描述。
除 `for` 中避免使用 `i`, `j`, `k`。

```objc
UIButton *settingsButton;
```
对于NSString,NSArray,NSNumber或BOOL:(无需后面指定类型)

```objc
NSString       *accountName;
NSMutableArray *mailboxes;
BOOL            userInputWasUpdated;
```

如果不是基本常用类型，要反应自身类型：

```objc
NSImage *previewPaneImage;
```

### 常量

常量名（如宏定义、枚举、静态局部变量等）应该以小写字母 k 开头，使用驼峰格式分隔单词，如：`kInvalidHandle`，`kWritePerm`。

### 图片资源命名

图片文件命名采用 `type_location_identifier_state` 规则

TODO

- icon
- btn
- bg
- line
- logo
- pic
- img

使用图片时候不要有 `.png` 后缀

**参考:**
```
UIImage *settingIcon = [UIImage imageNamed:@"icon_common_setting"];
```

## 注释

虽然写起来很痛苦，但注释是保证代码可读性的关键。下面的规则给出了你应该什么时候、在哪进行注释。记住：尽管注释很重要，但最好的代码应该自成文档。与其给类型及变量起一个晦涩难懂的名字，再为它写注释，不如直接起一个有意义的名字。

当你写注释的时候，记得你是在给你的听众写，即下一个需要阅读你所写代码的贡献者。大方一点，下一个读代码的人可能就是你！

## 文件注释

- 文件开头为 Xcode 自动生成注释，首行注释为文件名，要与实际文件名一致，文件名如有变化，首行注释要及时更新。
- 对于每个源文件要有维护人名称以及 Email 地址。
- 维护人只能是在职人员，交接工作时应更新维护人信息。

**例如:**

添加 `Owner` 行，格式要求 `Owner: [英文名、拼音名] - [电子邮件]`

```objc
//
//  COSViewController.h
//  Belle
//
//  Created by Cash on 14-6-29.
//  Copyright (c) 2014年 Cosmopolitan. All rights reserved.
//
//  Owner: Cash - wangwei@trends.com.cn
//
```

TODO: 声明部分的注释

TODO: 代码中的注释


## iOS 工程结构

**目录结构**

```
projectName/
    Resources                   图片等素材
    Sources                     代码
        /ViewController         控制器
        /Service                一些第三方比如支付宝，提供给controller的封装好的接口
        /External               引入的第三方库
        /Net                    网络请求
        /Model                  模型
        /Util                   工具类
        /Custom                 自定义的文件
            /Catergory          自定义的扩展类
            /Config             项目配置文件
            /View               视图
            /Util               工具类
```


## 参考内容
- [Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html#//apple_ref/doc/uid/10000146-SW1)
- [The official raywenderlich.com Objective-C style guide.](https://github.com/raywenderlich/objective-c-style-guide)
- [NYTimes Objective-C Style Guide](https://github.com/NYTimes/objective-c-style-guide)
- [Coding Guidelines for Cocoa (Github)](https://github.com/github/objective-c-conventions)
- [Google Objective-C Style Guide](http://google-styleguide.googlecode.com/svn/trunk/objcguide.xml)
- [Google 开源项目风格指南](http://zh-google-styleguide.readthedocs.org/en/latest/google-objc-styleguide/contents/)
- [编写高质量的Objective-C代码](http://www.cnblogs.com/xdream86/p/3309345.html)



=======================

###点标记语法###

属性和幂等方法使用点标记语法访问，其它情况用方括号标记语法。

例子：
```objc
view.backgroundColor = [UIColor orangeColor];

[UIApplication sharedApplication].delegate;
```





###数组和字典类型的字面值拆开
```
NSArray *number = @[@1, @2];
NSArray *string = @[@"ABC", @"XYZ"];

NSDictionary *dict = @{@"key1": @"value1",
                       @"key2": @123};
```





方法参数检查例子：
```
/**
 *  方法的注释
 */
- (void)someMethod
{
    if (!isRun) {
        return;
    }

    //Do something important;
}
```

###三元运算符###

三元运算符要有括号包裹，只能在变量赋值时候使用三元运算符
```
viewTitle = (title ? title : @"");
```


###有效性判断###
当一个方法通过引用返回一个错误参数，应该检测返回值的状态，而不是错误参数的状态。
```
NSError *error;

if (![self trySomethingWithError:&error]) {
    // Handle Error
}
```

###代理和block###

使用block还是delegate编写回调代码遵循以下几点：

- 如果对象存在多个不同事件，则应该使用代理模式编写各事件的处理代码
- 如果对象是单例，应该使用block，而不是代理。
- 如果对象是为了其他的信息而进行回调，则使用代理。
- 代理更多的是面向于过程，而block则更多的面向于结果。

block一般就set或init带进去，直接带参数不写通用（这样有提示防错），如果不带参数

```
@interface CustomModelViewController : BaseController <
    TTModelDelegate,
    TTURLRequestDelegate
>
```




##注释##

/**
 *  方法注释风格
 */


CGRect函数
CGRect frame = self.view.frame;
CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);

图片命名：

//  TODO:汪威

```
+ (instancetype)sharedInstance
{

   static id sharedInstance = nil;



   static dispatch_once_t onceToken;

   dispatch_once(&onceToken, ^{

      sharedInstance = [[self alloc] init];

   });



   return sharedInstance;

}

#define SYNTHESIZE_SINGLETON_FOR_CLASSNAME(classname) \
\
static classname *shared##classname = nil; \
\
+ (classname *)sharedInstance \
{ \
@synchronized(self) \
{ \
if (shared##classname == nil) \
{ \
shared##classname = [[self alloc] init]; \
} \
} \
\
return shared##classname; \
} \
\
+ (id)allocWithZone:(NSZone *)zone \
{ \
@synchronized(self) \
{ \
if (shared##classname == nil) \
{ \
shared##classname = [super allocWithZone:zone]; \
return shared##classname; \
} \
} \
\
return nil; \
} \
\
- (id)copyWithZone:(NSZone *)zone \
{ \
return self; \
} \
\
```

用#pragam mark- 分割

```
#pragma mark - Lifecycle

- (instancetype)init {}
- (void)dealloc {}
- (void)viewDidLoad {}
- (void)viewWillAppear:(BOOL)animated {}
- (void)didReceiveMemoryWarning {}

#pragma mark - Custom Accessors

- (void)setCustomProperty:(id)value {}
- (id)customProperty {}

#pragma mark - IBActions

- (IBAction)submitData:(id)sender {}

#pragma mark - Public

- (void)publicMethod {}

#pragma mark - Private

- (void)privateMethod {}

#pragma mark - Protocol conformance
#pragma mark - UITextFieldDelegate
#pragma mark - UITableViewDataSource
#pragma mark - UITableViewDelegate

#pragma mark - NSCopying

- (id)copyWithZone:(NSZone *)zone {}

#pragma mark - NSObject

- (NSString *)description {}
```





