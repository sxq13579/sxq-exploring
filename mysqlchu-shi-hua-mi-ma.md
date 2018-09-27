文章地址：https://blog.csdn.net/qq\_36955347/article/details/79182323

（1）如果之前装过mysql的，把mysql的server卸载掉，连带MySQL Server 5.7\data文件一起清干净

（2）重新装好后，输入net start mysql还是无法启动服务，这个时候，输入以下指令

 mysqld --remove 删除mysql服务

 mysqld --install 安装服务

 mysqld --initialize 初始化

net start mysql

然后发现服务已经启动

 \(3\)输入mysql -u root -p 启动mysql ，然后会要求你输入密码，注意由于是初始化的，所以系统自动配置一个初始化密码，这个密码在哪里找到呢？在MySQL Server 5.7.2\data这个路径下有一个计算机名字加err的文件，这个文件是错误日志，打开它，找到一个temporary password的记录条，冒号后面的就是初始化密码了。

 （4）输入初始化密码以后，修改密码，输入指令 alter user 'root'@'localhost' identified by '密码'；就能修改成功了。

 --------------------- 本文来自 开始淡漠 的CSDN 博客 ，全文地址请点击：https://blog.csdn.net/qq\_36955347/article/details/79182323?utm\_source=copy

