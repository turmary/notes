

# Remove '+' from kernel version

*	`LOCALVERSION` 可以在版本号之后追加后缀信息, 如果再定义  `CONFIG_LOCALVERSION_AUTO`, 将在最后进一步追加 `git` 版本号为后缀信息.

*	不定义`CONFIG_LOCALVERSION_AUTO` 将不显示 `git` 仓库信息, 如果此时 `LOCALVERSION` 变量定义也未定义, 将追加 "+".

*	如果既不想添加后缀, 又不想有 `"+"` 号 : 不定义`CONFIG_LOCALVERSION_AUTO`, 将 `LOCALVERSION` 变量定义为空 : `LOCALVERSION=`.

*	只要定义了 `LOCALVERSION`, 则就不会追加 "+" 号了

*	去掉git版本号也可以使用`echo "" > .scmversion`

[reference](https://github.com/gatieme/LDD-LinuxDeviceDrivers/tree/master/study/problem/build/local_version)

<br>

# Log level

|name | usage |
|--------|-------|
|console_loglevel|优先级高于(数值低于)该值的消息将被打印至控制台|
|default_message_loglevel|使用该优先级来打印未指定优先级的消息|
|minimum_console_loglevel|console_loglevel可被设置的最小值(最高优先级)|
|default_console_loglevel|N/A,未使用|

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
