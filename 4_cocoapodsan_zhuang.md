# cocoapods安装
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

#### 7.新建工程，并在终端用 cd 指令到文件夹内
$ pod search 第三方

#### 8.新建 Podfile 文件
$ touch Podfile

#### 9.编辑 Podfile 文件，并写入要添加的第三方库
platform:ios, '8.0'

pod 'AFNetworking', '~> 2.3.1'<-------第三方

#### 10.导入第三方库
$ pod install

#### 11.退出终端

