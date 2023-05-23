# 常用API、Lambda、常见算法





## 常用 API



### API 概述

* API(Application Programming interface)  应用程序编程接口。
* 简单来说：就是Java帮我们已经写好的一些方法，我们直接拿过来用就可以了。



### Object 类

* 一个类要么默认继承了Object类，要么间接继承了Object类，Object类是Java中的祖宗类。
* Object作为所有类的父类，提供了很多常用的方法给每个子类对象拿来使用。



#### toString 方法

> public String toString()
>
> 默认是返回当前对象在堆内存中的地址信息 : 类的全限名@内存地址

* 问题引出

  * 开发中直接输出对象，默认输出对象的地址其实是毫无意义的。

  * 开发中输出对象变量，更多的时候是希望看到对象的内容数据而不是对象的地址信息。

* 存在意义

  * 父类toString()方法存在的意义就是为了被子类重写，以便返回对象的内容信息，而不是地址信息！！ 



#### equals 方法

> public boolean equals(Object o)
>
> 默认是比较当前对象与另一个对象的地址是否相同，相同返回true，不同返回false

* 问题引出
  * 直接比较两个对象的地址是否相同完全可以用 “ == ” 替代equals。
  * 同时，开发中很多业务情况下，更想判断2个对象的内容是否一样。
* 存在意义
  * 为了被子类重写，以便子类自己来定制比较规则（比如比较对象内容）。



### Objects 类



####概述

* Objects是一个工具类，提供了一些方法去完成一些功能。



####常用方法

* equals（与上述equals略有不同，这个更安全）
  * public static boolean equals(Object a, Object b)
  * 比较两个对象的，底层会先进行非空判断，从而可以避免空指针异常。再进行equals比较
* isNull
  * public static boolean isNull(Object obj) 
  * 判断变量是否为null ,为null返回true ,反之false



### StringBuilder



#### 概述

* StringBuilder是一个可变的字符串的操作类，我们可以把它看成是一个对象容器。
* 使用StringBuilder的核心作用：操作字符串的性能比String要更高（如拼接、修改等）。
  * String 中的 + 操作也会创建 StringBuilder 对象



#### 构造器

* public StringBuilder()
  * 创建一个空白的可变的字符串对象，不包含任何内容
* public StringBuilder(String str)
  * 创建一个指定字符串内容的可变字符串对象



#### 常用方法

* public StringBuilder append(任意类型)
  * 添加数据并返回StringBuilder对象本身
  * 支持链式操作
* public StringBuilder reverse()
  * 将对象的内容反转
* public int length()
  * 返回对象内容长度
* public String toString()
  * 通过toString()就可以实现把StringBuilder转换为String



### Date 类



####概述

* Date类代表当前所在系统的日期时间信息。



#### 构造器

* public Date()
  * 创建一个Date对象，代表的是系统当前此刻日期时间。
* public Date(long time)
  * 把时间毫秒值转换成Date日期对象。



#### 常用方法

* public long getTime()
  * 返回从1970年1月1日    00:00:00走到此刻的总的毫秒数
* public void setTime(long time)
  * 设置日期对象的时间为当前时间毫秒值对应的时间



### SimpleDateFormat



#### 概述

* 代表简单日期格式化，可以用来把日期时间格式化成为我们想要的形式。



#### 构造器

* public SimpleDateFormat(String pattern)
  * 创建简单日期格式化对象，并封装格式化的形式信息



#### 常用方法

* public final String format(Date date)
  * 将日期格式化成日期/时间字符串
* public final String format(Object time)
  * 将时间毫秒值式化成日期/时间字符串
*  public Date parse(String source)
  *   从给定字符串的开始解析文本以生成日期



#### 格式化常用模式

*  y	年  
* M	月 
*  d	日  
* H	时  
* m	分  
* s	秒

> yyyy-MM-dd HH:mm:ss  
>
> yyyy年MM月dd日 HH:mm:ss  



### Calendar 类



#### 概述

* Calendar代表了系统此刻日期对应的日历对象。
* Calendar是一个抽象类，不能直接创建对象。



#### 创建对象的方法

* public static Calendar getInstance()
  * 获取当前日历对象



#### 常用方法

* public int get(int field)
  * 取日期中的某个字段信息。
* public void set(int field,int value)
  * 修改日历的某个字段信息。
* public void add(int field,int amount)
  * 为某个字段增加/减少指定的值
* public final Date getTime()
  * 拿到此刻日期对象。
* public long getTimeInMillis()
  * 拿到此刻时间毫秒值

> 注意：calendar是可变日期对象，一旦修改后其对象本身表示的时间将产生变化。



### JDK 8 新增日期类



#### 概述

* LocalDate：不包含具体时间的日期。
* LocalTime：不含日期的时间。
* LocalDateTime：包含了日期及时间。
* Instant：代表的是时间戳。
* DateTimeFormatter 用于做时间的格式化和解析的
* Duration:用于计算两个“时间”间隔 
* Period:用于计算两个“日期”间隔

> 新增的API严格区分了时刻、本地日期、本地时间，并且，对日期和时间进行运算更加方便。
>
> 其次，新API的类型几乎全部是不变类型（和String的使用类似），可以放心使用不必担心被修改。



#### LocalDate、LocalTime、LocalDateTime



#####概述

* 他们 分别表示日期，时间，日期时间对象，他们的类的实例是不可变的对象。
* 他们三者构建对象和API都是通用的



#####构建对象的方法

* public static Xxxx now();
  * 静态方法，根据当前时间创建对象
* public static Xxxx of(…);
  * 静态方法，指定日期/时间创建对象



##### 获取信息的API

* public int geYear()
  * 获取年
* public int getMonthValue()
  * 获取月份（1-12）
* Public int getDayOfMonth()
  * 获取月中第几天乘法
* Public int getDayOfYear()
  * 获取年中第几天
* Public DayOfWeek getDayOfWeek()
  * 获取星期



##### 转换相关API

* public LocalDate toLocalDate()
  * 转换成一个LocalDate对象
* public LocalTime toLocalTime()
  * 转换成一个LocalTime对象



##### 修改相关的API

> LocalDateTime 综合了 LocalDate 和 LocalTime 里面的方法，所以下面只用 LocalDate 和 LocalTime 来举例。
>
> 这些方法返回的是一个新的实例引用，因为LocalDateTime 、LocalDate 、LocalTime 都是不可变的。 

* plusDays, plusWeeks, plusMonths, plusYears
  * 向当前 LocalDate 对象添加几天、 几周、几个月、几年

* minusDays, minusWeeks, minusMonths, minusYears 
  * 从当前 LocalDate 对象减去几天、 几周、几个月、几年 
* withDayOfMonth, withDayOfYear, withMonth, withYear 
  * 将月份天数、年份天数、月份、年 份 修 改 为 指 定 的 值 并 返 回 新 的 LocalDate 对象 
* isBefore, isAfter 
  * 比较两个 LocalDate 



####Instant 时间戳

> 一个能表示一份数据在某个特定时间之前已经存在的、 完整的、 可验证的数据,通常是一个字符序列，唯一地标识某一刻的时间。

* JDK8获取时间戳特别简单，且功能更丰富。Instant类由一个静态的工厂方法now()可以返回当前时间戳。
* 时间戳是包含日期和时间的，与java.util.Date很类似，事实上Instant就是类似JDK8 以前的Date。
* Instant和Date这两个类可以进行转换。



#### DateTimeFormatter

* 在JDK8中，引入了一个全新的日期与时间格式器DateTimeFormatter。
* 正反都能调用format方法。

```java
LocalDateTime ldt = LocalDateTime.now();
System.out.println(ldt);//2021-03-01T15:09:17.444190900

DateTimeFormatter dtf = DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
String ldtStr = ldt.format(dtf);
System.out.println(ldtStr);//2021-03-01 15:09:17

String ldtStr1 = dtf.format(ldt);
System.out.println(ldtStr1);//2021-03-01 15:09:17
```



#### Period

* 在Java8中，我们可以使用以下类来计算日期间隔差异：java.time.Period
* 主要是 Period 类方法 getYears()，getMonths() 和 getDays() 来计算,只能精确到年月日。
* 用于 LocalDate 之间的比较。

```java
LocalDate today = LocalDate.now();
System.out.println(today);// 2021-03-01

LocalDate birthDate = LocalDate.of(1995, 1, 11);
System.out.println(birthDate); // 1995-01-11

Period period = Period.between(birthDate, today);
System.out.printf("年龄 : %d 年 %d 月 %d 日", period.getYears(),period.getMonths(), period.getDays());
```

>  Period：用于计算两个“日期”间隔。



#### Duration

* 在Java8中，我们可以使用以下类来计算时间间隔差异：java.time.Duration
* 提供了使用基于时间的值测量时间量的方法。
* 用于 LocalDateTime 之间的比较。也可用于 Instant 之间的比较。

```java
LocalDateTime today = LocalDateTime.now();
System.out.println(today);
LocalDateTime birthDate = LocalDateTime.of(1990,10,1,10,50,30);
System.out.println(birthDate);

Duration duration = Duration.between(birthDate, today);//第二个参数减第一个参数
System.out.println(duration.toDays());//两个时间差的天数
System.out.println(duration.toHours());//两个时间差的小时数
System.out.println(duration.toMinutes());//两个时间差的分钟数
System.out.println(duration.toMillis());//两个时间差的毫秒数
System.out.println(duration.toNanos());//两个时间差的纳秒数
```

>  Duration：用于计算两个“时间”间隔。 



#### ChronoUnit

* java.time.temporal.ChronoUnit
* ChronoUnit类可用于在单个时间单位内测量一段时间，这个工具类是最全的了，可以用于比较所有的时间单位

```java
LocalDateTime today = LocalDateTime.now();
System.out.println(today);
LocalDateTime birthDate = LocalDateTime.of(1990,10,1,10,50,30);
System.out.println(birthDate);

System.out.println("相差的年数：" + ChronoUnit.YEARS.between(birthDate, today));
System.out.println("相差的月数：" + ChronoUnit.MONTHS.between(birthDate, today));
System.out.println("相差的周数：" + ChronoUnit.WEEKS.between(birthDate, today));
System.out.println("相差的天数：" + ChronoUnit.DAYS.between(birthDate, today));
System.out.println("相差的时数：" + ChronoUnit.HOURS.between(birthDate, today));
System.out.println("相差的分数：" + ChronoUnit.MINUTES.between(birthDate, today));
System.out.println("相差的秒数：" + ChronoUnit.SECONDS.between(birthDate, today));
System.out.println("相差的毫秒数：" + ChronoUnit.MILLIS.between(birthDate, today));
System.out.println("相差的微秒数：" + ChronoUnit.MICROS.between(birthDate, today));
System.out.println("相差的纳秒数：" + ChronoUnit.NANOS.between(birthDate, today));

System.out.println("相差的半天数：" + ChronoUnit.HALF_DAYS.between(birthDate, today));
System.out.println("相差的十年数：" + ChronoUnit.DECADES.between(birthDate, today));
System.out.println("相差的世纪（百年）数：" + ChronoUnit.CENTURIES.between(birthDate, today));
System.out.println("相差的千年数：" + ChronoUnit.MILLENNIA.between(birthDate, today));
System.out.println("相差的纪元数：" + ChronoUnit.ERAS.between(birthDate, today));
```



## 包装类

* 对应于 8 种基本数据类型（Integer、Character）
* Java为了实现一切皆对象，为8种基本类型提供了对应的引用类型。
* 后面的集合和泛型其实也只能支持包装类型，不支持基本数据类型。

* 自动拆箱和装箱（语法糖）
  * valueOf
  * 源码
    * 常量池中有复用部分
* 特有功能
  * 包装类的变量的默认值可以是null，容错率更高。
  * 可以把基本类型的数据转换成字符串类型(用处不大)
    * 调用toString()方法得到字符串结果。
    * 调用Integer.toString(基本类型的数据)。
    * 其实可以 + ""
  * 可以把字符串类型的数值转换成真实的数据类型（真的很有用）
    * Integer.parseInt(“字符串类型的整数”)
    * Double.parseDouble(“字符串类型的小数”)。



##正则表达式



###匹配规则

* 字符类(默认匹配一个字符)
  * [abc]	       只能是a, b, 或c
  * [ ^ abc]	       除了a, b, c之外的任何字符
  * [a-zA-Z]               a到z A到Z，包括（范围）
  * [a-d[m-p]]	       a到d，或m通过p：（[a-dm-p]联合）
  * [a-z&&[def]]	       d, e, 或f(交集)
  * [a-z&&[ ^ bc]]	       a到z，除了b和c：（[ad-z]减法）
  * [a-z&& [ ^ m-p]]     a到z，除了m到p：（[a-lq-z]减法）
* 预定义的字符类(默认匹配一个字符)
  * .	任何字符
  * \d	一个数字： [0-9]
  * \D	非数字： [ ^ 0-9]
  * \s	一个空白字符： [ \t\n\x0B\f\r]
  * \S	非空白字符： [ ^ \s]
  * \w	[a-zA-Z_0-9] 英文、数字、下划线
  * \W	 [ ^ \w] 一个非单词字符
* 贪婪的量词（配合匹配多个字符）
  * X?	X , 一次或根本不
  * X*	X，零次或多次
  * X+	X , 一次或多次
  * X {n}	X，正好n次
  * X {n, }	X，至少n次
  * X {n,m}	X，至少n但不超过m次

> 不要随便出现空格



### 常用方法

*  public String replaceAll(String regex,String newStr)
  * 按照正则表达式匹配的内容进行替换
* public String[] split(String regex)：
  * 按照正则表达式匹配的内容进行分割字符串，反回一个字符串数组。
* public boolean matches(String regex): 
  * 判断是否匹配正则表达式，匹配返回true，不匹配返回false。



##Arrays 类

*  数组操作工具类，专门用于操作数组元素的。
* public static String toString(类型[] a)
  * 返回数组的内容（字符串形式）
* public static void sort(类型[] a)
  * 对数组进行默认升序排序
* public static < T > void sort(类型[] a, Comparator<? super T> c)
  * 使用比较器对象自定义排序
  * 比较规则：
    * 如果认为左边数据 大于 右边数据 返回正整数
    * 如果认为左边数据 小于 右边数据  返回负整数
    * 如果认为左边数据  等于 右边数据  返回0
* public static int binarySearch(int[] a, int key)
  * 二分搜索数组中的数据，存在返回索引，不存在返回 -1（或者包含更多信息的负数）



##Lambda 表达式



### 概述

* Lambda表达式是 JDK 8 开始后的一种新语法形式。 
* 作用：简化匿名内部类的代码写法。



### 基本格式

```java
(匿名内部类被重写方法的形参列表) -> {
    被重写方法的方法体代码。
}
注：-> 是语法形式，无实际含义
```

* 注意：
  * Lambda表达式只能简化函数式接口的匿名内部类的写法形式
* 函数式接口：
  * 首先必须是接口、其次接口中有且仅有一个抽象方法的形式
  * 通常我们见到的函数式接口上都有一个@FunctionalInterface注解，标记该接口必须是满足函数式接口。



### 省略写法（进一步简化）

* 参数类型可以省略不写。
* 如果只有一个参数，参数类型可以省略，同时()也可以省略。
* 如果Lambda表达式的方法体代码只有一行代码。可以省略大括号不写,同时要省略分号！
* 如果Lambda表达式的方法体代码只有一行代码。可以省略大括号不写。此时，如果这行代码是return语句，必须省略return不写，同时也必须省略";"不写
