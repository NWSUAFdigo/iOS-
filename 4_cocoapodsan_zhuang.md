# cocoapods安装与使用
### 一、 cocoapods安装

#### 1.开启 terminal
#### 2.移除现有 Ruby 默认源
$ gem sources --remove https://rubygems.org/

#### 3.使用新的源
$ gem sources -a https://ruby.taobao.org/

#### 4.验证新源是否替换成功
$ gem sources -l

#### 5.安装 CocoaPods
$ sudo gem install cocoapods

$ pod setup

备注：苹果系统升级 OS X EL Capitan 后安装改为:

$ sudo gem install -n /usr/local/bin cocoapods

$ pod setup

> pod setup需要等待的时间有些长，耐心等待，终端没有假死

#### 6.更新 gem
$ sudo gem update --system

### 二、 cocoapods使用

#### 1.新建工程，并在终端用 cd 指令到文件夹内
如下图：
![](屏幕快照 2016-06-02 上午10.12.19.png)

#### 2 搜索需要使用的第三方框架
$ pod search 第三方
- 如本图中搜索Masonry,可以使用：pod search Masonry
![](屏幕快照 2016-06-02 上午10.13.59.png)
- 按Q键退出vim，回到终端界面

#### 2.新建 Podfile 文件
$ touch Podfile

#### 3.编辑 Podfile 文件，并写入要添加的第三方库
platform:ios, '8.0'

pod 'AFNetworking', '~> 2.3.1'<-------第三方

#### 4.导入第三方库
$ pod install

#### 5.退出终端

