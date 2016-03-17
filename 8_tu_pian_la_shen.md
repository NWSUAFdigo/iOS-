# 图片拉伸
#### 1 简介
- 在iOS开发中，对于不同的图片，其拉伸的方式是不同的。

- 下图所示的就是一个聊天气泡，对于这种类型的图片，使用传统的拉伸显然是不合适的

  ![](屏幕快照 2016-03-17 下午5.11.55.png)
- 对于这种聊天气泡图片的放大，苹果提供了三种方式对其进行拉伸
- 图片拉伸所进行操作的对象是UIImage
  
#### 2 图片拉伸的方式一
```- (UIImage *)resizableImageWithCapInsets:(UIEdgeInsets)capInsets resizingMode:(UIImageResizingMode)resizingMode```
- 该方法是苹果最新推出的一种图片拉伸方法，于iOS6.0之后推出
- 需要使用一个UIImage对象来调用该方法
- 该方法返回一个新的UIImage对象
- 形参说明：
  - capInsets：该参数表示图片中可拉伸的范围，即哪些区域是会随着图片的放大而拉伸的，在拉伸范围外的图片内容就是受保护的，是不会随着图片的放大而拉伸的
  - resizingMode：拉伸模式。该方法提供了两中拉伸模式：UIImageResizingModeTile 平铺模式（**默认模式**、 UIImageResizingModeStretch 拉伸模式
- 可拉伸范围需要我们使用```UIEdgeInsetsMake(CGFloat top, CGFloat left, CGFloat bottom, CGFloat right)```方法来进行设置，其各个参数在图片中的表现如下图：

  ![](屏幕快照 2016-03-17 下午5.31.24.png)
  - 图中的绿色部分就是可拉伸的区域
  - 图中的蓝色部分就是受保护的区域，该区域是不会被拉伸的
  - top\left\bottom\right表示的是图像的各个边相对于对应边来说，向内部嵌入的距离。
  - 如：UIEdgeInsetsMake(10,20,10,15)就表示top边向内嵌入10个点距离，left边向内嵌入20个点距离，bottom边向内嵌入10个点距离，right边向内嵌入15个点距离
- **平铺模式下图像拉伸的规则**
  - 
  



