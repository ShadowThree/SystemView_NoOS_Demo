## 参考
1. `SystemView`安装路径: `SystemView/Doc/UM08027_SystemView.pdf`;
2. [官方文档：Use_SystemView_without_RTOS](https://wiki.segger.com/Use_SystemView_without_RTOS);

## 移植
1. 将`SystemView`安装路径下的`SystemView/Src`文件夹复制到工程中；
2. 将如下头文件路径添加到工程：
```c
SystemView/Config       // SystemView/Src/Config
SystemView/SEGGER       // SystemView/Src/SEGGER
```
3. 将如下源文件添加到工程：
```c
SystemView/Sample/NoOS/Config/Cortex-M/SEGGER_SYSVIEW_Config_NoOS.c
SystemView/SEGGER/SEGGER_RTT.c
SystemView/SEGGER/SEGGER_SYSVIEW.c
```
4. 在`MDK --> Options for Target --> C/C++`中，使能`GNU extensions`;
5. 在`SEGGER_SYSVIEW_Conf.h`中添加如下定义：
```c
// 注意：在 SEGGER_SYSVIEW_ConfDefaults.h 文件中，已经有如下定义：
// #define SEGGER_SYSVIEW_CORE_OTHER   0
// #define SEGGER_SYSVIEW_CORE_CM0     1 // Cortex-M0/M0+/M1
// #define SEGGER_SYSVIEW_CORE_CM3     2 // Cortex-M3/M4/M7
// #define SEGGER_SYSVIEW_CORE_RX      3 // Renesas RX

#define SEGGER_SYSVIEW_CORE	SEGGER_SYSVIEW_CORE_CM3
```
6. 按照`[main.c](./Core/Src/main.c)`的方式使用`SystemView`的`API`:
- 在需要监测的函数前后调用`SEGGER_SYSVIEW_Recordxxx()`和`SEGGER_SYSVIEW_RecordEndCall()`；(不同的函参对应不同的`API`)
- 在需要监测的中断前后调用`SEGGER_SYSVIEW_RecordEnterISR()`和`SEGGER_SYSVIEW_RecordExitISR()`;
7. 编译并烧录运行，然后在电脑上打开`SystemView`，并点击左上角工具栏中的绿色三角形即可；

## 说明
1. 必须使用`J-Link`才能使用`SystemView`;
2. `JLink`只需要通过`SWDIO`，`SWCLK`以及`GND`三根线和`MCU`连接;
3. `RTT`可以同时用于`RTT`日志输出和`SystemView`事件记录；但是输出的日志还是要用`J-Link RTT Viewer`才能看到，不知道为什么`SystemView`的`Terminal`窗口看不到日志；
4. 由于`SystemView`已经导入了`SEGGER_RTT.c`文件，所以使用[`dbger`](https://github.com/ShadowThree/dbger.git)就不用再导入这个文件了；

## ERROR: SystemView Overflow
1. 将`SystemView`的记录停止，重新开始记录试试；
2. 在`SysTick_Handler`中断处理函数中加上`SEGGER_SYSVIEW_TickCnt++;`
3. 将`SEGGER_RTT_Conf.h`中的`BUFFER_SIZE_UP`加大；
