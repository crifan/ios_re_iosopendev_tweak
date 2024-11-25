# PrivateFramework directory not found XCode iPhoneOS15.0.sdk

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
