
# ssh免密登录

在`Xcode`+`iOSOpenDev`的编译安装最后阶段，涉及到，自动通过ssh访问iPhone设备，把生成的`.deb`插件的文件下载和安装到iPhone中

此时就需要先准备好环境：确保`Mac`中可以，ssh的免密登录iPhone

此处ssh免密登录的具体步骤是：

* 先用ssh登录一次iPhone
  * 命令
    ```bash
    ssh root@192.168.1.27
    ```
  * 输入密码
    * `OpenSSH`的默认密码是：`alpine`
  * 即可登录到iPhone中
* 把ssh的key拷贝到iPhone中
  * 命令
    ```bash
    ssh-copy-id root@192.168.1.27
    ```
  * 输入密码：`alpine`

即可实现，ssh免密登录：

以后ssh直接可以访问iPhone，而无需输入密码
