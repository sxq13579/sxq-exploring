同步：

如果在代码块上加上synchronized关键字，则此代码块就被称为同步代码块。

可以使用synchronized关键字将一个方法声明成同步方法。

Java中方法定义的完整格式：

{public\|default\|protected\|private} {final} \[static\] \[synchronized\]

返回值类型void 方法名称\(参数类型 参数名称, ......\) \[throws Exception1, Exception2\] {

        \[return \[返回值\|返回调用处\]\]

 }

死锁：两个县城都在等待彼此先完成，造成了程序的停滞，一般程序的死锁都是在程序运行时出现的。

Object类对线程的支持：

wait\(\)线程等待

notify\(\)唤醒第一个等待的线程

notifyAll\(\)唤醒全部等待的线程



