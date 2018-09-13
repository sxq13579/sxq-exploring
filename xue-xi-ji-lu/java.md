**Timer类：**一种线程设施，可以用来实现在某一个时间或某一段时间后安排某一个任务执行一次或定期重复执行

cancel\(\)：用来终止该计数器，并放弃所有已安排的任务，对当前正在执行的任务没有影响

purge\(\)：将所有已经取消的任务移除，一般用来释放内存空间

schedule\(\)：安排一个任务在指定时间执行，如果已经超过该事件，则立即执行

scheduleAtFixedRate\(\)：安排一个任务在指定的时间执行，然后以近似固定的频率重复执行

**TimerTask类**：执行具体的任务

cancel\(\)：用来终止该任务

run\(\)：该任务索要执行的具体操作，该方法为引入的接口Runnable中的方法，子类需要覆写此方法

public long scheduledExecutionTime\(\)：返回最近一次要执行该任务的时间

File类：

pathSeparator：表示路径的分隔符（windows是：";"）；

separator：表示路径的分隔符（windows是："\"）;

createNewFile\(\) throws IOException

delete\(\)：删除文件

exists\(\)：判断文件是否存在

idDirectory\(\)：判断给定的路径是否是一个目录

publiv long length\(\)：返回文件的大小

public String\(\) list\(\)：列出指定目录的全部内容，只是列出了名称

public File\(\) listFiles\(\)：列出指定目录的全部内容，会列出路径

public boolean mkdir\(\)：创建一个目录

public boolean renameTo\(File dest\)：为已有的文件重新命名



