# copy
copy属于NSObject类中的一个方法，用于将一个对象复制一份。与其相对应的还有一个mutableCopy方法
#### 1 前提
- 任何操作系统，都提供了复制粘贴功能，复制可以将一个文件生成一个副本，并且两个文件的内容相同。同时修改其中一个文件的内容，不会影响到另一个文件的内容
- OC中的复制和文件复制类似，也是生成一个新的副本

#### 2 copy与mutableCopy
- 相同点
  - 两个方法都会对一个对象进行复制
- 不同点
  - copy方法会生成一个不可变的对象，如NSString，NSArray，NSDictionary
  - mutableCopy方法会生成一个可变对象，如NSMutableString，NSMutableArray，NSMutableDictionary
- 如果被拷贝的对象是一个可变对象，那么copy与mutableCopy都会生成一个新的对象，分别是一个新的可变对象和一个新的不可变对象
  - 例：
  ```objc
   NSMutableString * string = [NSMutableString string];
   [string appendString:@"12"];
        
   NSString * str1 = [string copy];
   NSMutableString * str2 = [string mutableCopy];
  ```
  - 首先生成了一个可变字符串对象，然后通过指针string指向该对象
  - 如果通过copy进行复制，那么系统会生成一个不可变字符串对象，并通过str1指向该对象
  - 如果通过mutableCopy进行复制，那么系统会生成一个可变字符串对象，并通过str2指向该对象
  - 此时string、str1、str2分别指向了一个对象，并且是不同的对象，对任何一个对象修改均不会影响到其他对象的值
- 如果被拷贝的对象是一个不可变对象，那么copy与mutableCopy是有区别的，copy将不会生成一个新的不可变对象，而是生成一个指针，指向了被拷贝的不可以按对象；而mutableCopy会生成一个新的可变对象
  - 例：
  ```objc
  NSString * string = @"123";
  NSString * str1 = [string copy];
  NSMutableString * str2 = [string mutableCopy];
  ```
  - 此时通过copy将不会生成新对象，而就是被拷贝对象，也就是@“123”
  - 也就是说，此时string和str1指向了同一块内存对象，它们存储的地址是一样的
  - 通过mutableCopy将会生成一个新的可变对象，所以string和str2中存储的地址是不同的
- 苹果之所以这样做是因为：**给定一个对象是不可变对象，那么如果通过copy生成的对象是一个新的不可变对象，则被拷贝对象和拷贝对象的内容相同，且同样不可变，此时就造成了内存浪费。所以苹果让不可变对象的copy方法不生成一个新的不可变对象**

#### 3 总结
| 源对象类型 | 拷贝方法 | 副本对象类型 | 是否产生了新对象 | 拷贝类型 |
| --  | -- | -- | -- | -- |
| NSString | copy | NSString | NO | 浅拷贝（指针拷贝） |
| NSString | mutableCopy | NSMutableString | YES | 深拷贝（内容拷贝） |
| NSMutableString | copy | NSString | YES | 深拷贝（内容拷贝） |
| NSMutableString | mutableCopy | NSMutableString | YES | 深拷贝（内容拷贝） |
| NS* | copy | NS* | NO | 浅拷贝（指针拷贝） |
| NS* | mutableCopy | NSMutable* | YES | 深拷贝（内容拷贝） |
| NSMutable* | copy | NS* | YES | 深拷贝（内容拷贝） |
| NSMutable* | mutableCopy | NSMutable* | YES | 深拷贝（内容拷贝） |
- 注：浅拷贝即拷贝一个指针，不生成新的对象；深拷贝即拷贝一个对象，生成一个新的对象

#### 4 自定义类如何实现copy功能
copy方法理论上可以在任何继承自NSObject的类中使用，但是如果是一个自定义类，直接使用copy方法将会出现错误
- 自定义类直接使用copy的错误说明
  - 如果一个自定义类直接使用copy，将会在编译的时候出错
  - 例：
  ```objc
  Person * p = [[Person alloc] init];      
  Person * p1 = [p copy];
  ```
  - Person是一个自定义类，如果直接将上面两句话编译，将会报错，错误原因如下：```reason: '-[Person copyWithZone:]: unrecognized selector sent to instance 0x100600080'```
  - 未找到Person类的copyWithZone：方法
  - 说明如果想要使用copy方法，必须要先实现copyWithZone：方法
- copyWithZone方法
  - ```- (id)copyWithZone:(NSZone *)zone；```
  - 该方法是NSCopying协议中的一个方法，而且是必须实现的方法
  - 所以可以推断，如果想要使用copy方法，那么自定义类必须要遵守NSCopying协议，并且实现copyWithZone方法
  - 该方法的返回值就是copy方法的返回值。也就是说，如果想让自定义类通过copy方法后返回一个复制的对象，就必须在该方法中实现复制方法
  ```objc
  -(id)copyWithZone:(NSZone *)zone{
    
    Person * p = [[Person alloc] init];
    
    p.age = self.age;
    
    p.name = self.name;
    
    return p;
  }
  ```
  - 此时再调用copy方法时，就会调用自定义类的copyWithZone方法，创建一个对象，将属性值赋值给新的对象，然后返回该对象
  - NSZone是一个空间对象，该方法实际上已将帮我们创建好了一个内存空间zone，所以不必再通过alloc来开辟新的内存空间。代码改进如下：
  ```objc
  -(id)copyWithZone:(NSZone *)zone{
    
    Person * p = [[Person allocWithZone:zone] init];
    
    p.age = self.age;
    
    p.name = self.name;
    
    return p;
}
  ```
- mutableCopy与copy方法类似，需要遵守NSMutableCopying协议，并实现相关方法

#### 5 copy在@property属性中的使用
正常情况下，如果一个属性是OC对象（带*号），那么可以使用strong关键字修饰；如果一个属性是非OC对象，那么可以使用assign属性。但是NSString字符串有些特殊
- **一般情况下，NSString字符串作为属性时，用copy取代strong来修饰该属性**
- 因为copy作为关键字时，属性的setter方法和使用strong时是有区别的
- 例：
  - 当字符串使用strong作为关键字时，其setter方法的声明和实现如下：
  ```objc
  // 声明
  @property (nonatomic,strong) NSString * name;
  // 实现
  -(void)setName:(NSString *)name{
    _name = name;
}
  ```
  此时属于正常的setter方法，当对name属性赋值时，实际上是讲name指针指向了赋值字符串
  - 当字符串使用copy作为关键字时，其setter方法的声明和实现如下：
  ```objc
  // 声明
  @property (nonatomic,copy) NSString * name;
  // 实现
  -(void)setName:(NSString *)name{
    _name = [name copy];
}
  ```
  实际上调用的是赋值字符串的copy方法
    - 这样做的好处就是保证了：无论赋值字符串是NSString还是NSMutableString，最终的name属性永远是NSString
    - 并且保证了name属性和赋值对象是相对独立的（赋值对象是NSString时，name属性也指向了这个对象，并且name属性是NSString；赋值对象是NSMutableString时，name属性指向了一个新的对象，并且是NSString对象）
- **注意：copy属性只能用于不可变对象，而不能用于可变对象。**所以下面的属性语句是有问题的
  - ```@property (nonatomic,copy) NSMutableString * name;```
  - 因为copy关键字最终返回的都是不可变对象，此时如果对name属性调用NSMutableString的特有方法，程序就会崩溃
- copy关键字与strong关键字的区别
  - 由于copy只能用于不可变对象，一般用于NSString，所以两者的区别只限于NSString使用的情况
  - 如果赋值对象是NSString，那么使用copy和strong是没什么区别的，因为不会产生新的对象，并且属性指针也都指向了赋值对象
  - **两者真正的区别在与赋值对象是NSMutableString的情况。**此时，copy会产生一个新的NSString对象，而strong只是将属性指针指向了赋值对象NSMutableString。所以**此时copy返回的是一个全新NSString对象，而strong返回的是NSMutableString赋值对象**
- NSArray、NSDictionary的情况比较复杂，分一层复制和二层复制，后续会讲到