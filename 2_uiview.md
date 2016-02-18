#  UIView

## 1 UIView是所有控件的父类，所有的控件最终均会继承自UIView

## 2 Apple将所有控件的基本属性都封装到UIView中，如frame，bounds，backgroundColor

## 3 每个控件都可以作为一个父控件，将其他控件作为其子空间放入该控件里面
> 注意：

> 1 每一个控制器内部都有一个默认的UIView控件，该控件的大小是整个手机屏幕，所有的控件都是该控件的子控件