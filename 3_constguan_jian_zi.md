#const关键字
#### 1 const关键字作用
- 如果在一个变量的声明前面加上const关键字，那么这个变量就变成了一个常量
- 例： const CGFloat pointA = 0.5;
- 此时，pointA的值就是0.5，不会再发生变化
- 在全局变量前加上const关键字就是全局常量，在局部变量前面加上const关键字就是局部常量
- const一般用在全局变量中
- const关键字的作用与#define宏定义非常相似，两者都是用来声明一个常量

#### 2 const与#define
```objc
const CGFloat pointA = 0.5;
#define pointA 0.5;
```
- 使用const和#define都可以定义一个常量，不过两者的实现方式是有区别的
- 宏定义就是一个简单的替换，会将文件中所有的pointA替换为0.5
- 所以本质上，pointA就是0.5，在所有用到pointA的地方，系统都会开辟一个局部常量0.5，作用域结束后再将其释放
- 宏定义只能在定义的文件中使用，其他文件如果想要使用该宏，只能引入该文件（宏如果定义在.m文件中，别的文件就无法访问）


- const会将修饰的变量变为常量，所以此时pointA是一个变量，并且是一个不可更改的变量（也就是常量），同时在内存中只有一份
- 此时在文件中使用的pointA都指向了同一份内存空间，而该内存空间会在程序运行结束后释放
- 如果是一个全局变量，通过const修饰后仍然是一个全局变量。可以在所有文件中访问（extern CGFloat pointA;），如果只是想在本文件中访问，可以在前面加上static关键字：static const CGFloat pointA = 0.5;

- 相较于#define，const显然更加合适定义常量，因为const不会存在内存空间的多次赋值和释放，在一定程度上提高了效率

#### 3 常量的定义和使用规范
在实际开发中，常量一般通过const来定义，并且定义在一个专门的文件中，此时声明的常量就是一个全局常量，在任何文件中都可以使用
- 由于全局变量或常量只要在一个文件中定义，所有文件都可以使用，所以将这些常量定义到一个文件中，一般选择一个空文件，然后将其命名为一个.m文件，如（WDConst.m）
```objc
#import <UIKit/UIKit.h>
const CGFloat pointA = 0.5;
```
- 将全局常量在WDConst.m文件中进行设置
- 然后在生成一个.h文件，如WDConst.h，用于将这些常量引用
```objc
#import <UIKit/UIKit.h>
extern CGFloat pointA;
```
- 此时如果想要使用pointA，只需要在头文件中引入WDConst.h文件，即可使用

- 注意：由于extern修饰的是全局变量，所以为了防止使用者误以为pointA可以修改，所以最好在extern后面加上const，表示这是一个全局常量
```objc
#import <UIKit/UIKit.h>
extern const CGFloat pointA;
```
- 此时外界引用时，如果修改pointA的值，在编译阶段就会报错
- 由于苹果在UIKit框架中对extern进行了一个宏定义，所以可以直接使用苹果定义的extern
```objc
#import <UIKit/UIKit.h>
UIKIT_EXTERN const CGFloat pointA;
```

#### 4 const修饰指针
对于一个指针，可以有两种操作方式：1 更改指针的指向 2 更改指针所指向的变量的值。在指针定义的过程中，const关键字放置的位置不同，对于指针的影响也是不同的。

| const放置位置 | 指针的指向 | 指针所指向的变量值 |
| -- | -- | -- |
| const int *p = &a | 可更改(p = &b;) | 不可更改(~~*p = 30;~~) |
| int const *p = &a | 可更改(p = &b;) | 不可更改(~~*p = 30;~~) |
| int * const p = &a | 不可更改(~~p = &b;~~) | 可更改(*p = 30;) |
- 在OC中，一般都是对指针进行修改（p），指针指向的地址很少去修改（*p），所以如果想让一个OC对象变为一个常量，最好是将其指针设置为不可修改