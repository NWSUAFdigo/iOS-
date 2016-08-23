# SizeClass
#### 1 在Xcode中的位置
![](屏幕快照 2016-08-23 上午10.56.37.png)
- 在main.storyboard文件中,位于interfaceBulider正下方的位置就是SizeClass的位置

#### 2 使用场景
如果想要对设备在横屏和竖屏时进行不同的布局,就需要使用到SizeClass
- 例:让一个UIView在iPhone横屏时位于屏幕左上方,iPhone竖屏时位于屏幕右下方,就需要使用SizeClass对其进行布局.使用autoLayout是无法实现这种需求的
- **注意:SizeClass只是提供了不同设备以及横屏和竖屏的不同布局方式,而具体的控件布局仍然需要使用autoLayout.所以有SizeClass必须有autoLayout,没有autoLayout必然没有SizeClass**

#### 3 如何使用
在SizeClass中,将iPhone和iPad的布局进行了统一,通过SizeClass的9个小方格的不同组合,就可以实现在不同设备之间,以及同一设备在横屏和竖屏之间的不同布局
- 宽度和高度
  - SizeClass对宽度和高度分别分为三种类型:Compact(紧凑),Any(任意),Regular(宽松)
  - 不同的宽度和高度组合就代表着不同的设备类型以及屏幕方向
  - Xcode默认启动后,SizeClass的宽度和高度分别是any和any,表示任何设备和屏幕方向都采用这种方式布局
  - ![](屏幕快照 2016-08-23 上午11.08.02.png)
  - 所以如果SizeClass的宽度和高度都是any,就相当于没有使用SizeClass.因为SizeClass的作用就是对不同的设备和屏幕方向进行不同的布局
- 常用的宽度和高度组合
  - 所有iPhone设备竖屏
    - ![](屏幕快照 2016-08-23 上午11.11.35.png)
  - 所有iPhone设备横屏
    - ![](屏幕快照 2016-08-23 上午11.13.37.png)
  - iPad设备横屏和竖屏
    - ![](屏幕快照 2016-08-23 上午11.14.53.png)
    - **注意:目前的SizeClass无法实现iPad在横屏和竖屏时分别布局,因为SizeClass没有提供这种宽高组合选项,如果要实现iPad在横竖屏的不同布局,只能使用代码**

#### 4 UIView在横竖屏使用不同布局
需求:添加一个UIView,在iPhone横屏时显示在屏幕左上方,在iPhone竖屏时显示在屏幕右下方
- 步骤
- 1 首先布局iPhone横屏
  - 1 调整SizeClass为iPhone横屏
  - 2 添加一个UIView
  - 3 设置UIView的约束为距离左边为0,距离顶部为0.并设置UIView的宽高值
  - ![](Snip20160823_7.png)
- 2 布局iPhone竖屏
  - 1 调整SizeClass为iPhone竖屏
  - ![](Snip20160823_8.png)
  - 2 此时已经添加的绿色View不见了,因为