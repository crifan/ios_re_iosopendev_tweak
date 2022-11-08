# 常见问题

## 安装器遇到了一个错误，导致安装失败

安装到最后，报错：`安装失败 安装器遇到了一个错误，导致安装失败`

![iosopendev_install_fail](../assets/img/iosopendev_install_fail.jpg)

解决办法：

其实此时`iOSOpenDev`的主体文件已安装到了默认的位置`/opt`中，接着去用工具初始化即可解决问题：

```bash
cd /opt/iOSOpenDevSetup/bin
sudo ./iod-setup base
sudo ./iod-setup sdk -sdk iphoneos
```

## PrivateFramework directory not found XCode iPhoneOS15.0.sdk

`iod-setup sdk -sdk iphoneos`时报错：

```bash
➜  bin sudo ./iod-setup sdk -sdk iphoneos
Setting up iPhoneOS 15.0 SDK...
Modifying SDK settings...
Symlinking to private frameworks header files...
PrivateFramework directory not found: /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS15.0.sdk/System/Library/PrivateFrameworks
```

原因：

此处是比较新的`XCode 13`和对应的`iOS 15`

->而最新版XCode和iOS早已将私有库PrivateFrameworks移走了

->即`iPhoneOSxx.xx.sdk/System/Library/`下面没有`PrivateFrameworks`了

解决办法：

* 自己之后是否用到私有库PrivateFrameworks
  * 否
    * 直接新建一个空目录即可
      ```bash
      cd /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS15.0.sdk/System/Library
      sudo mkdir PrivateFrameworks
      ```
  * 是
    * 除了新建目录外，还要把相关iPhoneOS版本的私有库的内容放过去
      * 先要找到相关iPhoneOS的PrivateFrameworks
        * 举例
          * `iPhoneOS 9.2`的`sdk`，可以从这里下载到：
            * [zhangkn/knPrivateFrameworks: /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/SDKs/iPhoneOS9.2.sdk/System/Library/PrivateFrameworks (github.com)](https://github.com/zhangkn/knPrivateFrameworks)

## File not found XCode Specifications iPhoneOSPackageTypes.xcspec

`iod-setup sdk -sdk iphoneos`报错：

```bash
➜  bin sudo ./iod-setup sdk -sdk iphoneos
Password:
Setting up iPhoneOS 15.0 SDK...
Modifying SDK settings...
Symlinking to private frameworks header files...
Adding specifications to platform...
File not found: /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/Specifications/iPhoneOSPackageTypes.xcspec
```

原因：

找不到specifications

解决办法：

下载别人给的：

* 4个iPhoneOS的spec文件
* 4个iPhoneSimulator的spec文件

分别放到对应位置，即可。

下载来源：

* 来源1：
  * [iosopendev专用Specifications.zip](https://www.ianisme.com/download/201605/iosopendev%E4%B8%93%E7%94%A8Specifications.zip)
* 来源2：
  * [越狱开发:用iosOpenDev配置越狱开发环境 编写第一个hello world_我的杯洗具的博客-CSDN博客](http://blog.csdn.net/u013583789/article/details/50396747)

下载后，可以看到Specifications中有8个spec。

分别新建Specifications目录：

```bash
sudo mkdir /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/Specifications
sudo mkdir /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/Library/Xcode/Specifications
```

再去

* 移动文件
  * 把
    * 4个`iPhoneOS`的文件
      * iPhoneOSPackageTypes.xcspec
      * iPhoneOSPackageTypes.xcspec.iOSOpenDev
      * iPhoneOSProductTypes.xcspec
      * iPhoneOSProductTypes.xcspec.iOSOpenDev
    * 放到：
      * /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/Specifications
  * 把：
    * 4个`iPhoneSimulator`的文件
      * iPhone Simulator PackageTypes.xcspec
      * iPhone Simulator PackageTypes.xcspec.iOSOpenDev
      * iPhone Simulator ProductTypes.xcspec
      * iPhone Simulator ProductTypes.xcspec.iOSOpenDev
    * 放到：
      * /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/Library/Xcode/Specifications

放好后是：

```bash
➜  Xcode ll /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneOS.platform/Developer/Library/Xcode/Specifications
total 48
-rwxr-xr-x@ 1 crifan  wheel   3.2K 12 24  2015 iPhoneOSPackageTypes.xcspec
-rwxr-xr-x@ 1 crifan  wheel   5.4K 12 24  2015 iPhoneOSPackageTypes.xcspec.iOSOpenDev
-rwxr-xr-x@ 1 crifan  wheel   4.0K 12 24  2015 iPhoneOSProductTypes.xcspec
-rwxr-xr-x@ 1 crifan  wheel   6.4K 12 24  2015 iPhoneOSProductTypes.xcspec.iOSOpenDev
➜  Xcode ll /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/Library/Xcode/Specifications
total 48
-rwxr-xr-x@ 1 crifan  wheel   3.4K 12 24  2015 iPhone Simulator PackageTypes.xcspec
-rwxr-xr-x@ 1 crifan  wheel   6.9K 12 24  2015 iPhone Simulator PackageTypes.xcspec.iOSOpenDev
-rwxr-xr-x@ 1 crifan  wheel   3.4K 12 24  2015 iPhone Simulator ProductTypes.xcspec
-rwxr-xr-x@ 1 crifan  wheel   6.1K 12 24  2015 iPhone Simulator ProductTypes.xcspec.iOSOpenDev
```

另外，新建usr的bin目录：

```bash
sudo mkdir /Applications/Xcode.app/Contents/Developer/Platforms/iPhoneSimulator.platform/Developer/usr/bin
```

即可。