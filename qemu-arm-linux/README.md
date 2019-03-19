# QEMU ARM Linux
https://people.debian.org/~aurel32/qemu/armhf/

***
## Download
```shell
    curl -SL -o vmlinuz-3.2.0-4-vexpress https://people.debian.org/~aurel32/qemu/armhf/vmlinuz-3.2.0-4-vexpress
    curl -SL -o initrd.gz-3.2.0-4-vexpress https://people.debian.org/~aurel32/qemu/armhf/initrd.img-3.2.0-4-vexpress
    curl -SL -o debian_wheezy_armhf_standard.qcow2  https://people.debian.org/~aurel32/qemu/armhf/debian_wheezy_armhf_standard.qcow2
```

***
## Run
### Windows Command Prompt
```shell
    qemu-system-arm -M vexpress-a9 -kernel vmlinuz-3.2.0-4-vexpress -initrd initrd.gz-3.2.0-4-vexpress -drive if=sd,file=debian_wheezy_armhf_standard.qcow2 -append "root=/dev/mmcblk0p2"
```
### Git BASH on Windows
```shell
    qemu-system-arm -M vexpress-a9 -kernel vmlinuz-3.2.0-4-vexpress -initrd initrd.gz-3.2.0-4-vexpress -drive if=sd,file=debian_wheezy_armhf_standard.qcow2 -append "root=//dev//mmcblk0p2"
```
