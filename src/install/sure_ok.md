# 确认安装成功

## 环境变量

再去确认，是否把iOSOpenDev的相关环境变量，加到启动脚本（此处是`zsh`，所以是`./zshrc`）中了：

```bash
➜  ~ cat ~/.zshrc | grep iOSOpenDev
export iOSOpenDevPath=/opt/iOSOpenDev
export iOSOpenDevDevice=
export PATH=/opt/iOSOpenDev/bin:$PATH
```

如果没有：

```bash
✘ crifan@licrifandeMacBook-Pro  /opt/iOSOpenDevSetup/bin  cat ~/.zshrc | grep iOSOpenDev
```

则自己手动去加上：

```bash
crifan@licrifandeMacBook-Pro  /opt/iOSOpenDevSetup/bin  vi ~/.zshrc
crifan@licrifandeMacBook-Pro  /opt/iOSOpenDevSetup/bin  cat ~/.zshrc | grep iOSOpenDev
export iOSOpenDevPath=/opt/iOSOpenDev
export iOSOpenDevDevice=
export PATH=/opt/iOSOpenDev/bin:$PATH
crifan@licrifandeMacBook-Pro  /opt/iOSOpenDevSetup/bin  source ~/.zshrc
```

## Xcode中的iOSOpenDev的模板

确认是否有多出的template模板：

```bash
➜  ~ ll ~/Library/Developer/Xcode/
total 0
drwxr-xr-x  8 crifan  staff   256B 10 14 11:13 DerivedData
srwxr-xr-x  1 crifan  staff     0B 10 27 08:54 GPUToolsAgent.sock
drwxr-xr-x  3 crifan  staff    96B 10 27 08:49 Templates
drwxr-xr-x  6 crifan  staff   192B 10 26 22:37 UserData
drwxr-xr-x  5 crifan  staff   160B  9 30 22:11 iOS Device Logs
drwxr-xr-x  4 crifan  staff   128B 10 13 13:54 iOS DeviceSupport
➜  ~ ll ~/Library/Developer/Xcode/Templates
total 0
lrwxr-xr-x  1 root  staff    25B 10 27 08:49 iOSOpenDev -> /opt/iOSOpenDev/templates
```

此处是有的：

* 多出了软链接：
  * `~/Library/Developer/Xcode/Templates/iOSOpenDev`
    * 指向的是：
      * `/opt/iOSOpenDev/templates`

以及接着去看看，具体有哪些模板：

```bash
➜  ~ ll /opt/iOSOpenDev/templates
total 48
drwxr-xr-x   5 root  wheel   160B 10 27 08:32 Action Menu Plugin.xctemplate
drwxr-xr-x   6 root  wheel   192B 10 27 08:32 Activator Listener.xctemplate
drwxr-xr-x  12 root  wheel   384B 10 27 08:32 AssistantExtensions Extension.xctemplate
drwxr-xr-x   4 root  wheel   128B 10 27 08:32 Base.xctemplate
drwxr-xr-x   6 root  wheel   192B 10 27 08:32 CaptainHook Tweak.xctemplate
drwxr-xr-x   6 root  wheel   192B 10 27 08:32 Cocoa Touch Library.xctemplate
drwxr-xr-x   5 root  wheel   160B 10 27 08:32 Command-line Tool.xctemplate
drwxr-xr-x   4 root  wheel   128B 10 27 08:32 Debian Package.xctemplate
drwxr-xr-x   4 root  wheel   128B 10 27 08:32 Empty Project.xctemplate
-rw-r--r--   1 root  wheel    18K 10 27 08:49 LICENSE
drwxr-xr-x   6 root  wheel   192B 10 27 08:32 Logos Tweak.xctemplate
drwxr-xr-x   5 root  wheel   160B 10 27 08:32 ManPage.xctemplate
drwxr-xr-x  11 root  wheel   352B 10 27 08:32 NotificationCenter Widget.xctemplate
drwxr-xr-x  12 root  wheel   384B 10 27 08:32 PreferenceLoader Bundle.xctemplate
drwxr-xr-x   7 root  wheel   224B 10 27 08:32 PreferenceLoader.xctemplate
-rw-r--r--   1 root  wheel   352B 10 27 08:49 README.md
drwxr-xr-x   5 root  wheel   160B 10 27 08:32 SBSettings Toggle.xctemplate
drwxr-xr-x   4 root  wheel   128B 10 27 08:32 Unit Tests.xctemplate
drwxr-xr-x   7 root  wheel   224B 10 27 08:32 XPC Service.xctemplate
```

很明显，部分模板，应该就是对应着界面中看到的各个模板：

比如：

* `Logos Tweak.xctemplate` -> `Logos Tweak`
* `Command-line Tool.xctemplate` -> `Command-line Tool`
* `PreferenceLoader Bundle.xctemplate` -> `PreferenceLoader Bundle`

## iOSOpenDev中的内容

顺带再去看看，当前iOSOpenDev目录中的内容：

```bash
➜  /opt ll
total 0
drwxr-xr-x  9 root  wheel   288B 10 27 08:32 iOSOpenDev
drwxr-xr-x  3 root  wheel    96B 10 27 08:32 iOSOpenDevSetup
drwxr-xr-x  3 root  wheel    96B 10 27 08:32 iOSOpenDevUninstall
➜  /opt cd iOSOpenDev
➜  iOSOpenDev pwd
/opt/iOSOpenDev
➜  iOSOpenDev ll
total 48
-rw-r--r--   1 root  wheel    18K 10 27 08:49 LICENSE
-rw-r--r--   1 root  wheel   352B 10 27 08:49 README.md
drwxr-xr-x   6 root  wheel   192B 10 27 08:32 bin
drwxr-xr-x   2 root  wheel    64B 10 27 08:32 frameworks
drwxr-xr-x   8 root  wheel   256B 10 27 08:32 include
drwxr-xr-x   5 root  wheel   160B 10 27 08:32 lib
drwxr-xr-x  21 root  wheel   672B 10 27 08:32 templates
➜  iOSOpenDev ll bin
total 3000
-rwxr-xr-x  1 root  wheel   428K 10 27 08:49 class-dump
-rwxr-xr-x  1 root  wheel   628K 10 27 08:49 class-dump-z
-rwxr-xr-x  1 root  wheel    59K 10 27 08:49 iosod
-rwxr-xr-x  1 root  wheel   383K 10 27 08:49 ldid
➜  iOSOpenDev ll frameworks
➜  iOSOpenDev ll include
total 48
drwxr-xr-x   3 root  wheel    96B 10 27 08:32 ActionMenu
drwxr-xr-x   3 root  wheel    96B 10 27 08:32 AssistantExtensions
drwxr-xr-x   3 root  wheel    96B 10 27 08:32 CaptainHook
drwxr-xr-x  10 root  wheel   320B 10 27 08:32 libactivator
drwxr-xr-x   3 root  wheel    96B 10 27 08:32 logos
-rw-r--r--   1 root  wheel    21K 10 27 08:49 substrate.h
➜  iOSOpenDev ll lib
total 1216
-rwxr-xr-x  1 root  wheel    77K 10 27 08:49 libactionmenu.dylib
-rwxr-xr-x  1 root  wheel   422K 10 27 08:49 libactivator.dylib
-rwxr-xr-x  1 root  wheel   101K 10 27 08:49 libsubstrate.dylib
➜  iOSOpenDev ll templates
total 48
drwxr-xr-x   5 root  wheel   160B 10 27 08:32 Action Menu Plugin.xctemplate
drwxr-xr-x   6 root  wheel   192B 10 27 08:32 Activator Listener.xctemplate
drwxr-xr-x  12 root  wheel   384B 10 27 08:32 AssistantExtensions Extension.xctemplate
drwxr-xr-x   4 root  wheel   128B 10 27 08:32 Base.xctemplate
drwxr-xr-x   6 root  wheel   192B 10 27 08:32 CaptainHook Tweak.xctemplate
drwxr-xr-x   6 root  wheel   192B 10 27 08:32 Cocoa Touch Library.xctemplate
drwxr-xr-x   5 root  wheel   160B 10 27 08:32 Command-line Tool.xctemplate
drwxr-xr-x   4 root  wheel   128B 10 27 08:32 Debian Package.xctemplate
drwxr-xr-x   4 root  wheel   128B 10 27 08:32 Empty Project.xctemplate
-rw-r--r--   1 root  wheel    18K 10 27 08:49 LICENSE
drwxr-xr-x   6 root  wheel   192B 10 27 08:32 Logos Tweak.xctemplate
drwxr-xr-x   5 root  wheel   160B 10 27 08:32 ManPage.xctemplate
drwxr-xr-x  11 root  wheel   352B 10 27 08:32 NotificationCenter Widget.xctemplate
drwxr-xr-x  12 root  wheel   384B 10 27 08:32 PreferenceLoader Bundle.xctemplate
drwxr-xr-x   7 root  wheel   224B 10 27 08:32 PreferenceLoader.xctemplate
-rw-r--r--   1 root  wheel   352B 10 27 08:49 README.md
drwxr-xr-x   5 root  wheel   160B 10 27 08:32 SBSettings Toggle.xctemplate
drwxr-xr-x   4 root  wheel   128B 10 27 08:32 Unit Tests.xctemplate
drwxr-xr-x   7 root  wheel   224B 10 27 08:32 XPC Service.xctemplate
```
