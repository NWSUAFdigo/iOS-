#  Auto Layout代码实现（VFL）
#### 1 VFL简介
Visual Format Language 可视化格式语言：该语言是苹果公司推出的专门针对Auto Layout约束的一种轻量化语言
#### 2 调用VFL创建约束对象的方法
+ (NSArray<__kindof NSLayoutConstraint *> *)constraintsWithVisualFormat:(NSString *)format options:(NSLayoutFormatOptions)opts metrics:(nullable NSDictionary<NSString *,id> *)metrics views:(NSDictionary<NSString *, id> *)views;
