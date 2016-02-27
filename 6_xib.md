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
   - 此时创建了一个名为WDBlockView.xib的文件，并且在文件中添加了一个View视图控件，视图控件中包含一个名为image的ImageView控件和一个名为name的Label控件

2 向控制器中添加xib文件
   - 与资源文件类似，xib文件也需要通过一些方法来添加到ViewController控制器中
   - xib添加的两种方式
    - 方式1
    ```objc
     NSBundle * bundle = [NSBundle mainBundle];
    NSString * path = [bundle pathForResource:@"WDBlockView.xib" ofType:nil];
    NSArray * xibArray = [NSArray arrayWithContentsOfFile:path];
    NSArray * xibArray = [bundle loadNibNamed:@"Test" owner:nil options:nil];
    NSLog(@"%@",xibArray); // 得到一个包含xib文件中所有控件的数组
    [self.view addSubview:xibArray[1]];
    ```
    - 方式2
    ```objc
    //UINib * nib = [UINib nibWithNibName:@"WDBlockView" bundle:[NSBundle mainBundle]];
    UINib * nib = [UINib nibWithNibName:@"WDBlockView" bundle:nil];
    NSArray * xibArray2 = [nib instantiateWithOwner:nil options:nil];
    NSLog(@"%@",xibArray2);
    [self.view addSubview:xibArray2[0]];
    ```
    
    - 注意：
    >1 xib文件是面向开发过程中的一个文件类型，xib文件在编译后将会变成nib文件，因此xib的许多方法中都包含nib
    >
    >2 无法使用pathForResource: ofType: 方法来从mainBundle中获得xib文件
    >
    >3 当方法的形参是```NSBundle *``` 类型时，可以通过nil表示mainBundle。方式2中nib的创建可以改为：```UINib * nib = [UINib nibWithNibName:@"Test" bundle:nil]; ```    
     