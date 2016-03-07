#  Auto Layout代码实现（Masonry）
#### 1 Masonry简介
Masonry是GitHub上一个非常有名的第三方框架，该框架是对苹果官方的Auto Layout代码进行封装，并提供一种更为简便的代码实现Auto Layout的方案
- 查找方法
  - 在GitHub上搜索masonry，点击第一个SnapKit/Masonry就是Masonry框架

#### 2 安装方法
![](屏幕快照 2016-03-07 下午3.01.47.png)
1. 在GitHub上找到Masonry，点击Download ZIP，下载整个框架包
2. 框架包中与框架同名的文件夹就是整个框架的内容，本例中框架包中的Masonry就是整个框架的内容
3. 将Masonry文件夹拖拽到Xcode项目中
4. 在需要引用该框架的文件中导入框架头文件 #import "Masonry.h" 就可以使用框架了

> 在后续中可以使用CocoaPod方法来导入框架，给内容后续说明

#### 3 使用方法
每一个框架包中都包含了该框架的使用方法说明
- 点击框架中的Readme.md文件可以查看作者对于框架的大致说明
- 点击 Masonry.xcworkspace 就可以将整个框架在Xcode中打开。可以点击框架中的示例查看框架如何使用