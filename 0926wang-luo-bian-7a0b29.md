ServerSocket类和Socket类

ServerSocket类主要用在服务器端程序的开发商，用于接收客户端的连接请求。

public ServerSocket\(int port\) throws IOException

public Socket accept\(\) throws IOException

public InetAddress getInetAddress\(\)

public boolean isClosed\(\)

public void close\(\) throws IOException

Socket表示一个客户端对象。

Public Socket\(String host, int port\) throws UnknownHostException,IOWxception

public InputStream getInputStream\(\) throws IOException

public OutputStream getOutputStream\(\) throws IOException

public void close\(\) throws IOException

public boolean isClosed\(\)



Channel本身是一个接口：

void close\(\) throws IOException关闭通道

boolean isOpen\(\)判断此通道是否是打开的

FileChannel是Channel的子类，可以进行文件的读\写操作。

public int read\(ByteBuffer dst\) throws IOException：将内容读入到缓冲区中

public int write\(ByteBuffer src\) throws IOException：将内容从缓冲区写入到通道

public final void close\(\) throws IOException：关闭通道

public abstract MappedByteBuffer map\(FileChannel, MapMode, long position, long size\) throws IOException

编码器\(CharseEncoder\)和解码器\(CharseDecoder\)



