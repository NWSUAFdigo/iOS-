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