#  Auto Layout代码实现（VFL）
#### 1 VFL简介
Visual Format Language 可视化格式语言：该语言是苹果公司推出的专门针对Auto Layout约束的一种轻量化语言

#### 2 调用VFL创建约束对象的方法
```+ (NSArray<__kindof NSLayoutConstraint *> *)constraintsWithVisualFormat:(NSString *)format options:(NSLayoutFormatOptions)opts metrics:(nullable NSDictionary<NSString *,id> *)metrics views:(NSDictionary<NSString *, id> *)views;```
- 使用NSLayoutConstraint类名调用该方法
- 参数含义：
  - 返回值：包含给定VFL的所有约束对象的一个数组
  - VisualFormat：VFL，使用字符串表示
  - options：约束类型，一般为空
  - metrics：VFL中具体数值，该参数使用一个字典表示，也就是用字典中的Value来替代VFL中表示数值的Key。注意数值为基本数据类型，必须封装为一个对象
  - views：VFL中所列出的控件对象，该参数使用字典表示，也就是用字典中的Value来代替VFL中表示控件的Key
- 示例代码：
  ```objc
  NSString * view1Vfl1 = @"H:|-[view1]-xxx-|";
  // 关于VFL的写法，可以在官方文档中输入“Visual Format Syntax”进行详细查看
  NSDictionary * view1Dict = NSDictionaryOfVariableBindings(view1);
  // 该函数用于创建一个Key名和Value名相同的字典
  NSArray * view1Constraint = [NSLayoutConstraint constraintsWithVisualFormat:view1Vfl1
                                                    options:kNilOptions
                                                    metrics:@{@"xxx":@20}
                                                    views:view1Dict];
  [view1.superview addConstraints:view1Constraint];
  ```
  
#### 3 VFL写法
- 格式： @"方向:|-距离-[控件(长度)]-距离-[控件(长度)]-距离-|";
- 说明：
  - 方向：包含H或者V，表示水平或垂直，该信息必须写入
  - 距离：控件的边缘到另一个控件边缘的距离，如果距离为0则省略 -距离-，如：H:|[view1(==20)]，如果距离为默认，则省略 距离- ，如：H:|-[view1]。默认距离约为18-19
  - 长度：控件的高度或者宽度，如果没有限制宽高，则不写

#### 4 注意事项
- VFL中一旦包含乘除法就会崩溃，例如让view2的宽度等于view1的宽度乘以0.5在VFL中很难实现
  ```objc
  NSString * view2VflH = @"H:[view2(==view1*0.5)]-|";
  NSDictionary * view2Dict = NSDictionaryOfVariableBindings(view1,view2);
  NSArray * view2ConstraintH = [NSLayoutConstraint constraintsWithVisualFormat:view2VflH 
                                                   options:kNilOptions 
                                                   metrics:nil 
                                                   views:view2Dict];
 [view2.superview addConstraints:view2ConstraintH];
  ```
    - 该段代码一旦执行，立即崩溃
- VFL和传统的创建NSLayoutConstraint约束对象可以进行混编来达到对控件进行约束的目的
   ```objc
   NSLayoutConstraint * view2Leading = [NSLayoutConstraint constraintWithItem:view2
                                                            attribute:NSLayoutAttributeLeading
                                                            relatedBy:NSLayoutRelationEqual
                                                            toItem:view2.superview
                                                            attribute:NSLayoutAttributeCenterX
                                                            multiplier:1.0
                                                            constant:0];
    [view2.superview addConstraint:view2Leading];
    
    NSString * view2VflH = @"H:[view2]-20-|";
    NSDictionary * view2Dict = NSDictionaryOfVariableBindings(view1,view2);
    NSArray * view2ConstraintH = [NSLayoutConstraint constraintsWithVisualFormat:view2VflH
                                                     options:kNilOptions
                                                     metrics:nil
                                                     views:view2Dict];
    [view2.superview addConstraints:view2ConstraintH];
   ```