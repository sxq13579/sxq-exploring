**Date类（java.util.Date）**

**Calendar类**（可以将取得的事件精确到毫秒），子类是GregorianCalendar类

getInstance\(\)：根据默认的时区实例化对象

after\(Object when\)：判断一个日期是否在指定日期之后

before\(Object when\)：判断一个日期是否在指定日期之前

get\(int field\)：返回给定日历字段的值

**DateFormat类**（和MessageFormat类都属于Format类的子类）

public static final DateFormat getDateInstance\(\)：得到对象

public staitc final DateFormat getDateTimeInstance\(\)：得到日期时间对象

**SimpleDateFormat类**（经常用于将String变为Date型数据）

public SimpleDateFormat\(String pattern\)：通过一个制定的模板构造对象

public Date parse\(String source\) throws ParseException：将一个包含日期的字符串变为Date类型

public final String format\(Date date\)：将一个Date类型按照指定格式变为String类型

**Math类**（都是静态方法）

**Random类**随机数产生类

nextBoolean\(\)：随机生成boolean值

double nextDouble\(\)：随机生成double值

float nextFloat\(\)：随机生成float值

nextInt\(\)：随机生成int值

nextLong\(\)：随机生成long值

**NumberFormat类**（和MessageFormat类都属于Format类的子类）

数字的格式化类，即可以按照本地的风格习惯进行数据的显示

getAvailableLocales\(\)：返回所有语言环境的数组

NumberFormat getInstance\(\)：返回当前默认语言环境的数字格式

NumberFormat getCurrencyInstance\(\)：返回当前默认环境的货币格式

**DecimalFormat类**（NumberFormat类的一个子类）

**BigInteger类**

add\(\)  substract\(\)  multiply\(\)  dicide\(\)  max\(\)  min\(\)  divideAndRemainder\(\)

**BigDecimal类**

add\(\)  substract\(\)  multiply\(\)  divide\(\)

**Arrays类**（主要功能是实现数组元素得查找、数组内容的填充、排序等）

boolean equals\(int\[\] a1, int\[\] a2\)

void fill\(int\[\] a, int val\)

void sort\(int\[\] a\)

int binarySearch\(int\[\] a, int key\)

**Comparable接口**

**Observer类：**

addObserver\(Observer o\) ：添加一个观察者；

deleteObserver\(Observer o\)： 删除一个观察者；

setChanged\(\)：被观察者状态发生改变

notifyObserver\(Object arg\)：通知所有观察者状态改变

**Pattern类和Matcher类**（应用正则表达式必用）





