---
layout: post
title: "What's the meaning of '>/dev/null 2>&1'?"
category: 
tags:
- Linux
- Shell
---
{% include JB/setup %}

看到syslog里有这个 `(nagios) CMD (/dev/shm/.b/cutitas >/dev/null 2>&1)`
突然发现忘记 `>/dev/null 2>&1` 什么意思了，温习一下。

1. 在linux里的默认file descripter

0 = stdin 
1 = stdout 
2 = stderr

2. `>` 代表重定向

{% highlight bash %}
  > file # clear file content
{% endhighlight %}

3. `/dev/null` 空设备文件，用来丢弃输出结果的。

4. `2>` 表示stderr错误重定向

5. `&` 表示‘等同于’的意思。 `2>&1`表示2的结果等同于1

其实 `> /dev/null 2> &1` == `1> /dev/null 2> &1`

所以这个命令 `echo "xxx" > /dev/null 2>&1` 就是抛弃所有的输出结果，反正也看不到，要看去日志吧，如果你记了日志的话。

值得注意的地方：

`command > file 2>file` 与 `command > file 2>&1` 区别？

虽然同时输出到同一个文件，但是file会被打开两次, 这样stdout和stderr会互相覆盖, 这样写相当使用了FD1和FD2两个同时去抢占file的管道。
而command >file 2>&1 这条命令就将stdout直接送向file, stderr 继承了FD1管道后,再被送往file,此时,file 只被打开了一次,也只使用了一个管道FD1,它包括了stdout和stderr的内容。


从IO效率上,前一条命令的效率要比后面一条的命令效率要低,所以在编写shell脚本的时候,较多的时候我们会command > file 2>&1 这样的写法。