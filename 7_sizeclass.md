# SizeClass
#### 1 在Xcode中的位置
![](屏幕快照 2016-08-23 上午10.56.37.png)
- 在main.storyboard文件中,位于interfaceBulider正下方的位置就是SizeClass的位置

#### 2 使用场景
如果想要对设备在横屏和竖屏时进行不同的布局,就需要使用到SizeClass
- 例:让一个UIView在iPhone横屏时位于屏幕左上方,iPhone竖屏时位于屏幕右下方,就需要使用SizeClass对其进行布局.使用autoLayout是无法实现这种需求的
