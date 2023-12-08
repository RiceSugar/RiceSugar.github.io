---
title: "Linux笔记"
description: "学习Linux的笔记"
tags: [ "Linux" , "Note" ]
date: 2022-04-14
slug: "linux-note"
---

### 常用linux命令

```text
alias :进行一个赋值 
ls    :查看目录下的文件 某认为当前目录
pwd   :查看当前目录的路径
cd    :切换到其他的目录
cp    :拷贝文件  cp object  target
rm    :rm -rf /* 删除文件
mv    : 移动文件吧文件 从a 移动到b  mv a b
mkdir : 创建一个目录
touch : 创建一个文件
chmod : 修改文件的权限。
sudo  : 提权 提升用户的权限 
apt   : apt install
echo  : 打印 变量、字符串
cat   : 查看文件内容
ps    : 查看进程信息
kill  : 向指定进程 发送一个信号kill -9 PID 杀死一个进程
ping  : 检测网络的联通性
vim   : 文本编辑器
history: 查看过去的命令
passwd: 修改用户的密码
which: 用于查看 某个文件所在的目录
tail : tail 查看文件内容 尾部
head : tail| head -n 10
grep : 做一些正则表达 对内容进行匹配
whoami :查看当前用户
find  : 查找一个文件
wget  : 对网页请求
export: 设置环境变量
```

### cpp文件编译

- 预处理    编译      汇编         链接
`.c  --- >  .I  --- > .S   ----> .o   ---- > elf文件`
预处理: `gcc -E main.c -o main.i`
编译:    `gcc -S main.i -o main.s`
汇编：`gcc -c main.s -o main.o`
链接：`gcc main.o -o main / /`


### 生成静态库(.a文件)

- 生成.o文件 `gcc -c xxx.c -o xxx.o`

- 生成静态库 `ar -cr libxxx.a xxx.o`
    - ar：静态函数库创建的命令
    - -c :create的意思
    - -r :replace的意思，表示当前插入的模块名已经在库中存在，则替换同名的模块。如果若干模块中有一个模块在库中不存在，ar显示一个错误信息，并不替换其他同名的模块。默认的情况下，新的成员增加在库的结尾处。

- 使用静态库 `gcc -o main main.c -L(PATH) -lxxx（库名)`

### 生成动态库(.so文件)

- 生成.o文件 `gcc -c xxx.c - o xxx.o`

- 生成动态库 `gcc -shared -fPIC xxx.o -o libxxx.so`
    - -shared : 生成动态库
    - -fPIC : 生成位置无关的代码

- 使用动态库 `gcc -o main main.c -L(PATH) -lxxx（库名）`

- 动态库查找顺序：
  - 编译目标代码时指定的动态库搜索路径
  - 环境变量`LD_LIBRARY_PATH`指定的动态库搜索路径
  - 配置文件`/etc/ld.so.conf`中指定的动态库搜索路径
    - 在该文件尾部追加库所在的完整路径，如`"/root/test/conf/lib"`
    - 然后运行`sudo ldconfig`使修改生效。
  - 默认的动态库搜索路径`/lib` `/usr/lib`

- 连接动态库失败
  - 解决方法
    - 将文件`libxxx.so`复制到目录`/usr/lib`中
    - 将`libxxx.so`拷贝到可执行文件main的同一目录下