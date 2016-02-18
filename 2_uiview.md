#  UIView

## 1 UIView是所有控件的父类，所有的控件最终均会继承自UIView

## 2 Apple将所有控件的基本属性都封装到UIView中，如frame，bounds，backgroundColor

## 3 每个控件都可以作为一个父控件，将其他控件作为其子空间放入该控件里面
> 注意：

> 1 每一个控制器内部都有一个默认的UIView控件，该控件的大小是整个手机屏幕，所有的控件都是该控件的子控件

>![View](屏幕快照 2016-02-18 下午4.06.42.png)

> 2 在一个控制器相对应的 .m文件中，```self.view```就是调用控制器内部默认的UIView控件

>![View](屏幕快照 2016-02-18 下午4.10.11.png)

> 3 子控件的显示层级为：最下面的控件在最顶上显示，最上面的控件在最底层显示

## 4 常见属性
- ```@property(nonatomic,readonly) UIView * superview;```调用某个控件的父控件

- ```@property(nonatomic,readonly,copy) NSArray * subviews;```调用某个控件的所有子控件
    > 注意：数组下标越大的控件显示在越顶上*

- ```- (void)addSubview:(UIView *)view;```为某一个父控件添加子控件

- ```- (void)removeFromSuperview;```将某个控件从父控件中移除

- ```- (UIView *)viewWithTag:(NSInteger)tag;```通过tag值来需找父控件中的某个控件，其内部的实现原理如下(不一定准确，仅作说明)：
    ```objc
    if(self.view.tag == 99) 
    return self.view;
    for(UIView * view in self.view.subviews)
    {
        if(view.tag == 99)
        return view;
        break;
    }
    ```
    - 该方法表明，当父控件的tag值为某个数（如99）时，返回父控件
    - 当父控件的tag值不为给定的数值时，按照子控件在父控件中的位置从上至下（从0开始往下）查找，直到找到tag值为给定的数值时结束查找
    - 当子控件中有两个或以上的tag值符合要求时，会将子控件数组中最上面的那个控件返回 
    

- ```- (void)insertSubview:(UIView *)view aboveSubview:(UIView *)siblingSubview;```将某个控件插在另一个控件的上面

- ```- (void)insertSubview:(UIView *)view belowSubview:(UIView *)siblingSubview;```将某个控件插在另一个控件的下面
    > 注意

    > 上述两个方法中，aboveSubview是将控件插在另一个控件的上面，也就是插入的控件显示在顶上。belowSubview是将控件插在另一个控件的下面，也就是插入的控件显示在底下。
    
    > 所以aboveSubview中，插入的控件在子控件数组（subviews）中位于被插入控件的下面（后面）,而belowSubview中，插入的控件在子控件数组（subviews）中位于被插入控件的上面（前面）
    

- 调整控件位置的方法
    ```objc
    - (void)insertSubview:(UIView *)view atIndex:(NSInteger)index;
    // 将控件插入到指定索引的位置
    
    - (void)insertSubview:(UIView *)view belowSubview:(UIView *)siblingSubview;
    // 将控件插入到某个控件的下面
    
    - (void)insertSubview:(UIView *)view aboveSubview:(UIView *)siblingSubview;
    // 将控件插入到某个控件的上面
    
    - (void)bringSubviewToFront:(UIView *)view;
    // 将控件置顶，也就是插入到控件数组的最末尾
    
    - (void)sendSubviewToBack:(UIView *)view;
    // 将控件放置到底部，也就是在控件数组的下标为0 
    ```