## �ο�
1. `SystemView`��װ·��: `SystemView/Doc/UM08027_SystemView.pdf`;
2. [�ٷ��ĵ���Use_SystemView_without_RTOS](https://wiki.segger.com/Use_SystemView_without_RTOS);

## ��ֲ
1. ��`SystemView`��װ·���µ�`SystemView/Src`�ļ��и��Ƶ������У�
2. ������ͷ�ļ�·����ӵ����̣�
```c
SystemView/Config       // SystemView/Src/Config
SystemView/SEGGER       // SystemView/Src/SEGGER
```
3. ������Դ�ļ���ӵ����̣�
```c
SystemView/Sample/NoOS/Config/Cortex-M/SEGGER_SYSVIEW_Config_NoOS.c
SystemView/SEGGER/SEGGER_RTT.c
SystemView/SEGGER/SEGGER_SYSVIEW.c
```
4. ��`MDK --> Options for Target --> C/C++`�У�ʹ��`GNU extensions`;
5. ��`SEGGER_SYSVIEW_Conf.h`��������¶��壺
```c
// ע�⣺�� SEGGER_SYSVIEW_ConfDefaults.h �ļ��У��Ѿ������¶��壺
// #define SEGGER_SYSVIEW_CORE_OTHER   0
// #define SEGGER_SYSVIEW_CORE_CM0     1 // Cortex-M0/M0+/M1
// #define SEGGER_SYSVIEW_CORE_CM3     2 // Cortex-M3/M4/M7
// #define SEGGER_SYSVIEW_CORE_RX      3 // Renesas RX

#define SEGGER_SYSVIEW_CORE	SEGGER_SYSVIEW_CORE_CM3
```
6. ����`[main.c](./Core/Src/main.c)`�ķ�ʽʹ��`SystemView`��`API`���ɣ�
7. ���벢��¼���У�Ȼ���ڵ����ϴ�`SystemView`����������Ͻǹ������е���ɫ�����μ��ɣ�

## ˵��
1. ����ʹ��`J-Link`����ʹ��`SystemView`;
2. `JLink`ֻ��Ҫͨ��`SWDIO`��`SWCLK`�Լ�`GND`�����ߺ�`MCU`����;