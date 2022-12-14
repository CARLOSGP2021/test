* CPU占用过高如何检测：

  1. 使用**top**命令找出CPU占比最高的进程PID；
  
  2. 查询进程中，哪个线程的cpu占用率高，记住TID：`ps -mp pid -o THREAD,tid,time`。
  
      其中，-m显示所有的线程，-p表示pid进程使用cpu的时间，-o表示该参数后是用户自定义格式，如：THREAD,tid,time表示线程、线程ID号、线程占用的时间。
  
  3. 将TID转换为16进制格式（英文小写格式） `printf “%x\n” tid`
  
  4. 通过`jstack`命令获取占用资源异常的线程栈：
  
      ```php
      jstack pid > jstack.pid.log #先保存文件，再从文件中查看
      或者
      jstack 514 |grep 202 -A 30  #直接命令行查看
      ```
  
  5. 从上面日志文件或者命令行查看日志，从日志中能看到自己编写的代码的类和方法，一般情况是对应代码处产生了死循环。

- kill和kill -9的区别

  kill和kill -9，两个命令在linux中都有杀死进程的效果。执行kill命令，系统会发送一个`SIGTERM`信号给对应的程序。程序接收到该信号后，会先释放自己的资源，然后再停止。但是也有程序可能接收信号后，做一些其他的事情（如果程序正在等待IO，可能就不会立马做出响应），也就是说，SIGTERM多半是会被阻塞的。而`kill -9`命令，系统给程序发送的信号是`SIGKILL`，即exit。exit信号不会被系统阻塞，所以kill -9能顺利杀掉进程。

- 用什么命令对一个文件的内容进行统计？(行号、单词数、字节数)

  wc 命令：- c 统计字节数 - l 统计行数 - w 统计字数。

- scp命令：本地和远程互传文件

 - 



- [Linux经典面试题总结_spring_root的博客-CSDN博客](https://blog.csdn.net/baidu_39322753/article/details/101016653)