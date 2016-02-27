# Xib
#### 1 Xib的创建
在Xcode左侧的导航栏中右键，选择New File,就会弹出如下对话框：
![](屏幕快照 2016-02-27 下午12.07.55.png)

选择User Interface，就会出现四个选项卡：
- Storyboard 创建一个storyboard文件
- View 创建一个含有一个UIView视图控件的xib文件
- Empty 创建一个xib文件，文件内部无空间
- Launch Screen 创建一个启动界面文件

其中选择**View**或者**Empty**就会创建一个**Xib**文件

#### 2 Xib文件的作用
xib文件与storyboard文件有许多的相似之处，但也有一些不同：
- 相同
    - 两者都可以通过图形化的方式（Interface bulider）来创建控件，并对控件的各项属性和位置等进行设置
    - 两者本质上都是xml文件，通过后期编译为纯代码的方式进行控件操作
- 不同
    - storyboard是一个重量级的，其负责的是整个界面的创建和控件添加
    - xib属于轻量级的，可以对某一个局部的视图进行专门的创建和控件添加
    
#### 3 Xib的使用方法
1 通过类似于storyboard的方法进行控件的创建，并进行属性设置
![](屏幕快照 2016-02-27 下午3.23.29.png)
   - 