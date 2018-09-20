Class类的常用方法：

public staic Class&lt;?&gt; forName\(String className\) throws ClassNotFoundException

public Constructor\[\] getConstructors\(\) throws SecurityException：取得一个类的全部构造方法

public Field\[\] getDeclaredFields\(\) throws SecurityException

public Method\[\] getMethods\(\) throws SecurityException：取得一个类的全部方法

public Method getMethods\(String name, Class... parameter Types\) throws NoSuchMethodException, SecurityException

public Class\[\] getInterfaces\(\)：取得一个类所实现的全部接口

public String getName\(\)

public Package getPackage\(\)

public Class getSuperclass\(\)：取得一个类的父类

public Object newInstance\(\) throws InstantiationException, IllegalAccessException

public Class&lt;?&gt; getComponentType\(\)

public boolean isArray\(\)

只是在操作时需要明确地调用类中的构造方法，并将参数传递进去之后才可以进行实例化操作。

Constructor类，表示的是构造方法

public int getModifiers\(\)

public String getName\(\)

public Class&lt;?&gt;\[\] getParameterTypes\(\)

public String toString\(\)

public T newInstance\(Object... initargs\) throws InstantiationException,IllegalAccessException,IllegalArgumentException,InvocationTargrtException

Methods类的常用方法：

public int getModifiers\(\)：取得方法的修饰符

public String getName\(\)：取得方法名称（包括继承来的方法）

public Class&lt;?&gt;\[\] getParameterTypes\(\)：返回全部参数类型

public Class&lt;?&gt; getReturnType\(\)：返回值类型

public Class&lt;?&gt;\[\] getExceptionTypes\(\)：取得全部的异常输出

public Object invoke\(Object obj, Object... args\) throws IllegalAccessException,IllegalArgumentException,InvocationTargetException

取得实现的接口或者父类中的公共属性：public Field\[\] getFields\(\) throws SecurityException

取得本类中的全部属性：public Field\[\] getDeclaredFields\(\) throws SecurityException

Fields类：

public Object get\(Object obj\) throws IllegalArgumentException,IllegalAccessException

public Object set\(Object obj, Object value\) throws IllegalArgumentException,IllegalAccessException

public int getModifiers\(\)：取得方法的修饰符

public String getName\(\)：取得方法名称（包括继承来的方法）

public boolean isAccessible\(\)：判断此属性是否可被外部访问

public static void setAccessible\(AccessibleObject\[\] array, boolean flag\) throws SecurityException

public String toString\(\)



