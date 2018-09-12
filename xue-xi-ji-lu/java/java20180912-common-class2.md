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







