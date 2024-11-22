# 如何新增(`.xm`和`.mm`)文件

有时候，需要去新增文件：`.xm`和`.mm`

具体步骤是：

* 新建`.xm`文件
  * 选中要新增文件所属的位置 -> 右键 -> `Add File`-> `iOS` -> `Other`->`Empty`->输入文件名：`yourFilename.xm` ->`Create`
* 编译 -> 会生成对应`.mm`文件
  * （先`Product`->`Clean Build Folder`，再）`Product`->`Build`
    * 会从`yourFilename.xm`生成`yourFilename.mm`
* 把`.mm`文件加到`Compile Sources`中
  * 右键-> `Add Files to {yourProjectName}` -> 选择（刚新生成的）`yourFilename.mm`
    * 项目文件列表中，即可新增对应文件`yourFilename.mm`
    * 项目的待编译的文件中，也包含了对应的`.mm`文件
      * `Targets`->`Build Phase`->`Compile Sources` 中有了刚加入的`.mm`文件
        * 如果文件，点击`加号`=`➕`，去新增导入进来
          * 这样后续编译代码时，才能真正编译到对应hook代码
