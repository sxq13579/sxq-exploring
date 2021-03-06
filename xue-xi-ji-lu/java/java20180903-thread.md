线程的状态：

1、创建状态：Thread thread = new Thread\(\);

2、就绪状态：当线程启动时，线程进入就绪状态；

3、运行状态：当就绪装药的线程被调用并获得处理器资源时，线程就进入了运行状态。

4、堵塞状态：当可执行状态下，如果调用sleep\(\)、suspend\(\)、wait\(\)等方法，线程都将进入堵塞状态。

5、死亡状态：线程调用stop\(\)方法时或run\(\)方法执行结束后，即处于死亡状态。

Java程序每次运行至少启动几个线程？

每当使用Java没命令执行一个类时，实际上都会启动一个JVM，每一个JVM实际上就是在操作系统中启动了一个进程，Java本身具备了垃圾的收集机制，所以在Java运行时至少会启动两个线程，一个是main线程，另一个是垃圾收集线程。

* isAlive\(\)方法可测试线程是否已经启动而且仍在启动。
* join\(\)方法让一个线程强制执行。
* Thread.sleep\(\)可实现休眠
* **setDaemon\(\)**
* setPriority方法可以设置一个线程的优先级（并非优先级越高就一定会先执行，那哪个线程先执行将由CPU的调度决定）
* yield\(\)方法将一个线程的操作暂时让给其他线程执行
* ~~suspend\(\)方法：暂时挂起线程~~
* ~~resume\(\)方法：恢复挂起的线程~~
* ~~stop\(\)方法：停止线程~~

同步与死锁

