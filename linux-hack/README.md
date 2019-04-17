

# Remove '+' from kernel version

*	`LOCALVERSION` 可以在版本号之后追加后缀信息, 如果再定义  `CONFIG_LOCALVERSION_AUTO`, 将在最后进一步追加 `git` 版本号为后缀信息.

*	不定义`CONFIG_LOCALVERSION_AUTO` 将不显示 `git` 仓库信息, 如果此时 `LOCALVERSION` 变量定义也未定义, 将追加 "+".

*	如果既不想添加后缀, 又不想有 `"+"` 号 : 不定义`CONFIG_LOCALVERSION_AUTO`, 将 `LOCALVERSION` 变量定义为空 : `LOCALVERSION=`.

*	只要定义了 `LOCALVERSION`, 则就不会追加 "+" 号了

*	去掉git版本号也可以使用`echo "" > .scmversion`

[reference](https://github.com/gatieme/LDD-LinuxDeviceDrivers/tree/master/study/problem/build/local_version)
