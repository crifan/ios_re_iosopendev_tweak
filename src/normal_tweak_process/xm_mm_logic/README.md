# 搞懂.xm和.mm文件的逻辑

此处，在真正，新增hook代码文件，写hook代码之前，要去：

搞懂`iOSOpenDev`中`.xm`和`.mm`文件的逻辑

此处核心内容是：

* `.xm`：原始的hook插件的代码
* `.mm`：从`.xm`自动（在`Build`后）自动生成的文件

->

* 所以 = 结果
  * iOSOpenDev新增（hook代码逻辑的）文件时
    * 是：`.xm`文件
    * 不是：`.mm`文件
  * 写hook插件=添加hook代码逻辑时，改动的文件
    * 是：`.xm`文件
    * 而不是：`.mm`文件
  * 你每次改动更新`.xm`后
    * iOSOpenDev内部会自动从最新的`.xm`生成最新的`.mm`文件
      * 因此，旧的`.mm`文件（的内容）会被新的`.mm`文件（的内容）覆盖掉
        * 所以即使，如果，你之前改动了`.mm`文件，也是没用的，会被覆盖掉的
  * Xcode最终去编译（内部其实是iOS的`clang`编译器）时
    * 不支持：`.xm`
      * 万一`Xcode`的`Compile Sources`中（由于失误而）加入了`.xm`文件，则会导致编译报错
        * 具体详见：[Compile Sources中误添加了不支持的.xm](../../common_issue/expected_unqualified_id/compile_sources_added_xm.md)
    * 只支持：`.mm`
      * 所以接下来，要去把`.mm`加到`Compile Souces`，供Xcode最终编译用
  * 首次（`Xcode`->`Build`）编译时，会从`.xm`，生成额外的`.mm`文件
    * 首次时=只用做一次
      * 概述
        * 需要你去`Xcode`->右键->`Add Files to`
        * 去把`.mm`文件加进来（导入进来，弹框选项记得选择：`Copy items if needed`
        * 此时，对应的`Xcode`->`Targets`->`Build Phases`->`Compile Sources`中，就可以看到对应的`.mm`文件了
      * 详见
        * [如何新增xm文件](../../normal_tweak_process/xm_mm_logic/new_xm_file.md)
    * 注
      * 后续则无需重复添加`.mm`文件
