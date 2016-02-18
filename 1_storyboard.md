#  storyboard

## 1 程序一旦启动，首先加载的是**`Main.storyboard`**的这个文件

> 注意：

>在以后的iOS开发中，一个程序可能有很多的.storyboard文件，但是在默认情况下只有名称为`Main`的storyboard文件才会在程序启动时首先执行

>当然也可以修改程序启动时所要加载的storyboard文件，在项目-->Target-->Main Inetrface中修改
![Main Interface](屏幕快照 2016-02-18 上午11.22.09.png)

>同时还需要将箭头指向该storyboard中的某一个ViewController,点击右侧属性面板中的Is Initial View Controller
![Initial View Controller](屏幕快照 2016-02-18 上午11.27.26.png)


## 2 IBAction的本质就是void，其特点就是让方法具有和Interface Bulider连线的功能

## 3 IBOutlet就是让属性具有连线功能

## 4 连线注意事项
- 1 连线与方法是相对应的
- 2 一个控件对象可以和多个方法进行连线，此时一个控件由多个方法进行监听
- 3 一个方法也可以和多个控件进行连线，此时一个方法可以监听多个控件，一般用于控件的功能相似的情况
- 4 当监听控件的方法被注释或者删除时，其相对应的控件的连线必须删除，否则对该控件进行操作时程序会崩溃
- 5 当控件在ViewController中的属性被注释或者删除时，其相对应的控件的连线同样必须删除，否则程序将无法启动

## 5 ViewController（视图控制器）
- 1 一个ViewController负责一个storyboard中的大界面，不要一对多，也不要多对一
- 2 ViewController负责它所控制的界面的控件创建、事件处理等


