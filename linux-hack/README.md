

# Remove '+' from kernel version

*	`LOCALVERSION` �����ڰ汾��֮��׷�Ӻ�׺��Ϣ, ����ٶ���  `CONFIG_LOCALVERSION_AUTO`, ��������һ��׷�� `git` �汾��Ϊ��׺��Ϣ.

*	������`CONFIG_LOCALVERSION_AUTO` ������ʾ `git` �ֿ���Ϣ, �����ʱ `LOCALVERSION` ��������Ҳδ����, ��׷�� "+".

*	����Ȳ�����Ӻ�׺, �ֲ����� `"+"` �� : ������`CONFIG_LOCALVERSION_AUTO`, �� `LOCALVERSION` ��������Ϊ�� : `LOCALVERSION=`.

*	ֻҪ������ `LOCALVERSION`, ��Ͳ���׷�� "+" ����

*	ȥ��git�汾��Ҳ����ʹ��`echo "" > .scmversion`

[reference](https://github.com/gatieme/LDD-LinuxDeviceDrivers/tree/master/study/problem/build/local_version)
