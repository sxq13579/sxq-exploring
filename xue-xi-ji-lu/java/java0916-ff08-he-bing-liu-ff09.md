合并流：将两个文件的内容合并成一个文件

public SequenceInputStream\(InputStream s1, InputStream s2\)

public int available\(\) throws IOException

压缩流：

JAR压缩输出流：JarOutputStream

JAR压缩输入流：JarInputStream

JAR文件：JARFile

JAR实体：JAREntry

GZIP是用于UNIX系统的文件压缩，在Linux中经常会使用到\*.gz的文件，就是GZIP格式，GZIP压缩的支持类保存在java.util.zip包中，常用类有如下两个：

GZIP压缩输出流：GZIPOutputStream

GZIP压缩输入流：GZIPInputStream



在Java中，没一个压缩文件都可以使用ZipFile表示，还可以使用ZipFile根据压缩后的文件名称找到每一个压缩文件中的ZipEntry并将其进行解压缩操作，ZipFile类的常见方法：

public ZipFile\(File file\) throws ZipException, IOException

public ZipEntry getEntry\(String name\)

public InputStream getInputStream\(ZipEntry entry\) throws IOException

public String getName\(\)

ZipInputStream类是InputStream的子类，通过此类可以方便地读取ZIP格式的压缩文件，此类的常用方法如表：

public ZipInputStream\(InputStream in\)

public ZipEntry getNextEntry\(\) throws IOException

