#  数据存储
- iOS应用程序中的数据存取工作是通过将数据存放到不同的目录中来完成的
- iOS应用程序数据存储的几种方式
  - xml属性列表文档（plist文件）：该文件一般存放数组和字典，并且成员必须是系统自带的类型，也就是说，自定义类型的数据是无法存放到plist文件中的
  - Preference(偏好设置)
  - NSKeyedArchiver归档(NSCoding)
  - SQLite3
  - Core Data
  - 后几项内容后续会讲到
- 在iOS中，每一个应用程序都有一个**沙盒**。每一个应用程序只能访问自己所在的沙盒，无法访问别的应用程序的沙盒，也就是说，**沙盒之间相互隔离**
- 一个应用程序的沙盒如下图所示：

![](图片 1.png)
- 先将各个部分依次进行说明

|  | 数据类型 | iTunes同步 | 管理方式 | 实例 |
| -- | -- | -- | -- | -- |
| Layer | mainBundle | -- | -- | 程序代码、图片资源、plist文件等 |
| Documents | 运行时生成的需要持久化的数据 | 同步 | 用户管理 | 游戏存档 |
| Caches | 运行时生成的需要持久化的数据 | 不同步 | 用户管理 | 体积大、不需要备份的非重要数据 |
| Preferences | 应用的所有偏好设置 | 同步 | 用户管理 | 应用的所有偏好设置 |
| tmp | 应用运行时所需的临时数据 | 不同步 | 系统管理 | 程序没有运行时，系统可能会清除该目录下的文件 |
- 说明
  - 在模拟器环境中，Layer存放在Bundle目录中，而其他数据存放到Data目录中
  - 数据一般存放在Documents和Caches两个目录中，tmp目录由于系统会进行清理，所以很少使用
- 沙盒中各个目录的访问方法
  - Layer：
  ```objc
  NSString * path = [[NSBundle mainBundle] bundlePath];
  ``` 
  - Documents：
  ```objc
  NSArray * doctArray = NSSearchPathForDirectoriesInDomains(NSDocumentDirectory, NSUserDomainMask, YES); 
  ```
    - NSSearchPathForDirectoriesInDomains函数说明
    - 该函数用来搜寻沙盒路径，其中需要传入三个形参
    - NSDocumentDirectory：该形参表明该函数需要寻找Document文件目录的路径
    - NSUserDomainMask：该形参表明在用户领域查找
    - YES：YES表明返回的是一个全路径
      - 如：/Users/NWSUAF/Library/Developer/CoreSimulator/Devices/88A5F96F-E2FE-4A71-8610-C97B0CDEF939/data/Containers/Data/Application/F798210B-FF97-41CA-9D42-B4281D20D6C0/Library/Caches
      - 如果是NO，则沙盒路径用~表示，如~/Library/Caches
  - Caches：
  ```objc
  NSArray * cachesArray = NSSearchPathForDirectoriesInDomains(NSCachesDirectory, NSUserDomainMask, YES);
  ```
  - Preferences：还没找到
  - tmp：
  ```objc
  NSString * tempPath = NSTemporaryDirectory();
  ```
  - 沙盒路径：
  ```objc
  NSString * sandBoxPath = NSHomeDirectory();
  ```
   