## 什么是 GDB

GDB 调试器，可以允许你在运行程序时检查里面发生了什么？

- 开始并设置参数
- 打断点 在特殊情况下停止
- 程序停止时，检查发生什么
- 支持跨平台

## 支持哪些语言

- Ada
- Assembly
- C
- C++
- D
- Fortran
- Go
- Objective-C
- OpenCL
- Modula-2
- Pascal
- Rust

## 搭建实验环境 安装 GDB

安装 GDB

```bash
sudo apt-get install  gdb
```

 检查是否成功安装

```bash
gdb --version
```

## QuickStart

写程序

```c
#include <stdio.h>

int main() {

	int arr[4] = {1, 2, 3, 4};
	int i = 0;
	for (i = 0; i < 4; i++) {
		printf("%d\n", arr[i]);
	}

	return 0;
}
```

* 编译：`gcc test.c`

* 编译加调试：`gcc -g test.c`

* 使用 gdb：`gdb ./a.out`

  * 运行：`r（run 简写）`
  * 退出 gdb：`quit`

  * 查看 gdb 常用命令：`man gdb`

  * 查看程序源代码：`list`

  * 打断点：`b（break 简写）`

    ​		函数名字

    ​		行号

  * 查看断点情况：`info b`

  * 打印变量：`p（print 简写）`

    ​		arr[0]

    ​		&arr[0]

  * 进入某一个具体的函数调试：`s（step 简写）`

**GDB 的小技巧**

* 使用 shell 去调用终端的命令

* 日志功能：`set logging on`

* watchpoint 观察变量是否变化

  ​		info 查看 watchpoint



## 调试 core 文件`

调试一个程序，程序挂掉 core

shell 做一些限制

core 文件 不会默认生成

ulimit -a

```bash
real-time non-blocking time  (microseconds, -R) unlimited
core file size              (blocks, -c) 0
data seg size               (kbytes, -d) unlimited
scheduling priority                 (-e) 0
file size                   (blocks, -f) unlimited
pending signals                     (-i) 15294
max locked memory           (kbytes, -l) 498056
max memory size             (kbytes, -m) unlimited
open files                          (-n) 1024
pipe size                (512 bytes, -p) 8
POSIX message queues         (bytes, -q) 819200
real-time priority                  (-r) 0
stack size                  (kbytes, -s) 8192
cpu time                   (seconds, -t) unlimited
max user processes                  (-u) 15294
virtual memory              (kbytes, -v) unlimited
file locks                          (-x) unlimited
```

man 手册

* 查看 core 文件：gdb 二进制文件 core文件

如果 core 文件没有生成，需要查看 ulimit 限制

## 调试一个正在运行的程序

* 查看进程：`ps -ef | grep a.out`

```c
#include <stdio.h>

// test test1
// i i++
// call test test1

void test() {

}

void test1() {
	int i = 0;
	i++;
}

int main() {
	for(;;) {
		test();
		test1();
	}
	return 0;
}
```

* 编译运行：`gcc -g test_for.c`
* 启动进程：`./a.out &`(& 是到后台运行)
* 调试：`gdb -p pid`



**GDB 官网地址**:  https://www.sourceware.org/gdb/