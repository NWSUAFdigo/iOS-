#const关键字
#### 1 const关键字作用
- 如果在一个变量的声明前面加上const关键字，那么这个变量就变成了一个常量
- 例： const CGFloat pointA = 0.5;
- 此时，pointA的值就是0.5，不会再发生变化
- 在全局变量前加上const关键字就是全局常量，在局部变量前面加上const关键字就是局部常量
- const关键字的作用与#define宏定义非常相似，两者都是用来声明一个常量

#### 2 const与#define
