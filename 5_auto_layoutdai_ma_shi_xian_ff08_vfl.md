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
