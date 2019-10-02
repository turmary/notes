

# Remove '+' from kernel version

*	`LOCALVERSION` �����ڰ汾��֮��׷�Ӻ�׺��Ϣ, ����ٶ���  `CONFIG_LOCALVERSION_AUTO`, ��������һ��׷�� `git` �汾��Ϊ��׺��Ϣ.

*	������`CONFIG_LOCALVERSION_AUTO` ������ʾ `git` �ֿ���Ϣ, �����ʱ `LOCALVERSION` ��������Ҳδ����, ��׷�� "+".

*	����Ȳ�����Ӻ�׺, �ֲ����� `"+"` �� : ������`CONFIG_LOCALVERSION_AUTO`, �� `LOCALVERSION` ��������Ϊ�� : `LOCALVERSION=`.

*	ֻҪ������ `LOCALVERSION`, ��Ͳ���׷�� "+" ����

*	ȥ��git�汾��Ҳ����ʹ��`echo "" > .scmversion`

[reference](https://github.com/gatieme/LDD-LinuxDeviceDrivers/tree/master/study/problem/build/local_version)

<br>

# Log level

|name | usage |
|--------|-------|
|console_loglevel|���ȼ�����(��ֵ����)��ֵ����Ϣ������ӡ������̨|
|default_message_loglevel|ʹ�ø����ȼ�����ӡδָ�����ȼ�����Ϣ|
|minimum_console_loglevel|console_loglevel�ɱ����õ���Сֵ(������ȼ�)|
|default_console_loglevel|N/A,δʹ��|

------

**Changed in cmdline**
  ```
  debug|quiet|loglevel=5
  ```

**Changed in printk.c**
  ```
  #undef CONSOLE_LOGLEVEL_DEFAULT
  #define CONSOLE_LOGLEVEL_DEFAULT 8
  ```

# Enable DEBUG
  ```patch
  --- a/drivers/mmc/core/Makefile
  +++ b/drivers/mmc/core/Makefile
  @@ -20,1 +20,2 @@ obj-$(CONFIG_MMC_TEST)         += mmc_test.o
   obj-$(CONFIG_SDIO_UART)                += sdio_uart.o
  +ccflags-y += -DDEBUG=1
  ```

**In C file begin**
  ```
  #define pr_fmt(fmt) KBUILD_MODNAME " %s():%d: " fmt, __func__, __LINE__
  ```
