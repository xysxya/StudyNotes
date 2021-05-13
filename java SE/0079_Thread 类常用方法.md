# Thread 类中常用方法

## void start()

启动线程，并执行线程下的 run() 方法。

## run()

通常是要重写，执行线程在被调度时的操作

## String getName()

返回线程的名称

## void setNmae(String name)

设置线程的名称

## static ThreadCurrent()

返回当前的线程。在 Thread 的子类中就是 this, 通常用于主线程和 Runnable 的实现。

## yield()

释放 CPU 的执行权

## jion()

在线程 a 中调用线程 b 的 jion() 方法，线程 a 会进入阻塞状态，直到线程 b 县城结束，a 的阻塞状态才会停止

## stop() 已过时

强制线程结束

## sleep(long millitime)

让当前线程睡眠，直到指定的时间 millitime 时间过去，线程才能继续进行

## isAlive()

判断线程是否还存活








