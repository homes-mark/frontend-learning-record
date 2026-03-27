# Math 类
```java
package math;

public class MathDemo {
    /*
        Math类 : 包含执行基本数字运算的方法

        --------------------------------------------------------------------
        public static int abs (int a) : 获取参数绝对值
        public static double ceil (double a) : 向上取整
        public static double floor (double a) : 向下取整
        public static int round (float a) : 四舍五入
        public static int max (int a, int b) : 获取两个int值中的较大值
        public static double pow (double a,double b) : 返回a的b次幂的值
        public static double random () : 返回值为double的随机值，范围[0.0,1.0)
        --------------------------------------------------------------------
     */
    public static void main(String[] args) {
        // public static int abs (int a) : 获取参数绝对值
        System.out.println(Math.abs(10));
        System.out.println(Math.abs(-10));
        System.out.println("---------------------------------");
        // public static double ceil (double a) : 向上取整
        System.out.println(Math.ceil(12.3));
        System.out.println(Math.ceil(12.9));
        System.out.println(Math.ceil(12.0));
        System.out.println("---------------------------------");
        // public static double floor (double a) : 向下取整
        System.out.println(Math.floor(12.3));
        System.out.println(Math.floor(12.9));
        System.out.println(Math.floor(12.0));
        System.out.println("---------------------------------");
        // public static int round (float a) : 四舍五入
        System.out.println(Math.round(12.3));
        System.out.println(Math.round(12.9));
        System.out.println("---------------------------------");
        // public static int max (int a, int b) : 获取两个int值中的较大值
        System.out.println(Math.max(10, 20));
        System.out.println(Math.min(10, 20));
        System.out.println("---------------------------------");
        // public static double pow (double a, double b) : 返回a的b次幂的值
        System.out.println(Math.pow(2, 3));
        System.out.println("---------------------------------");
        // public static double random () : 返回值为double的随机值，范围[0.0,1.0)
        System.out.println(Math.random());

    }
}

```

# System 类
```java
package system;

public class SystemDemo {
    /*
        System类常见方法 :

            1. public static void exit (int status) : 终止当前运行的 Java 虚拟机，非零表示异常终止
            2. public static long currentTimeMillis () : 返回当前系统的时间毫秒值形式
                                                                - 返回1970年1月1日 0时0分0秒, 到现在所经历过的毫秒值
                                                                - 返回1970年1月1日 8时0分0秒, 到现在所经历过的毫秒值

            3. public static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length) : 数组拷贝

                                                        1. 数据源数组
                                                        2. 起始索引
                                                        3. 目的地数组
                                                        4. 起始索引
                                                        5. 拷贝的个数
     */
    public static void main(String[] args) {
        int[] arr1 = {11, 22, 33, 44, 55};
        int[] arr2 = new int[3];

        System.arraycopy(arr1, 1, arr2, 0, 3);

        for (int i : arr2) {
            System.out.println(i);
        }
    }

    private static void method() {
        long start = System.currentTimeMillis();

        String s = "";

        for (int i = 1; i <= 100000; i++) {
            s += i;
        }

        System.out.println(s);


        long end = System.currentTimeMillis();

        System.out.println(end - start);
    }
}

```

# 包装类
将基本数据类型，包装成类(变成引用数据类型)

> 变成类，就可以创建对象了对象就可以调用方法方便的解决问题了
>

<img src="https://cdn.nlark.com/yuque/0/2026/png/35081558/1774615571465-0ddb6096-2c93-4c19-baef-694ddc5b28d9.png" width="369" title="" crop="0,0,1,1" id="u7b1b5807" class="ne-image">

+ 手动装箱: 手动调用 `Integer.valueOf()` 方法, 将基本数据类型, 手动包装为类
+ 手动拆箱: 手动调用 Integer 中的 `intValue()` 方法, 将包装类对象, 转换为基本数据类型
+ 自动拆装箱: 基本数据类型和对应的包装类, 可以直接运算, 操作起来非常便捷

```java
package integer;

public class IntegerMethodDemo {
    /*
        Integer类的常见方法:

            public static String toBinaryString(int i)      得到二进制
            public static String toOctalString(int i)       得到八进制
            public static String toHexString(int i)         得到十六进制
            public static int parseInt(String s)            将字符串类型的整数转成int类型的整数

     */
    public static void main(String[] args) {
        System.out.println(Integer.toBinaryString(12));
        System.out.println(Integer.toOctalString(12));
        System.out.println(Integer.toHexString(12));

        int i = Integer.parseInt("123");
        System.out.println(i + 100);

        String s = "itheima";

        // Character中不存在 parseXxx方法, 其它的包装类都有.

        char c = s.charAt(0);
        char[] charArray = s.toCharArray();
        System.out.println(c);
        System.out.println(charArray);
    }
}

```

```java
package integer;

public class IntegerTest {
    /*
        已知字符串
        String s = "10,50,30,20,40";

        请将该字符串转换为整数并存入数组
        随后求出最大值打印在控制台
     */
    public static void main(String[] args) {
        String content = "10,50,30,20,40";
        String[] arr = content.split(",");
        int[] nums = new int[arr.length];

        for (int i = 0; i < arr.length; i++) {
            nums[i] = Integer.parseInt(arr[i]);
        }

        int max = nums[0];
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] > max) {
                max = nums[i];
            }
        }
        System.out.println("最大值为:" + max);
    }
}

```

# BigDecimal 类
用于解决小数运算中，出现的不精确问题

```java
package bigdecimal;

public class BigDicimalDemo {
    public static void main(String[] args) {
        double num1 = 0.1;
        double num2 = 0.2;
        // 0.30000000000000004
        System.out.println(num1 + num2);
    }
}

```

BigDecimal 类的使用

```java
package bigdecimal;

import java.math.BigDecimal;
import java.math.RoundingMode;

public class BigDecimalDemo2 {
    /*
        BigDecimal类 : 用于解决小数运算中, 出现的不精确问题

        BigDecimal创建对象 :

                public BigDecimal(double val) : 不推荐, 无法保证小数运算的精确
                ---------------------------------------------------------------
                public BigDecimal(String val)
                public static BigDecimal valueOf(double val)

        BigDecimal常用成员方法 :

                public BigDecimal add(BigDecimal b) : 加法
                public BigDecimal subtract(BigDecimal b) : 减法
                public BigDecimal multiply(BigDecimal b) : 乘法
                public BigDecimal divide(BigDecimal b) : 除法
                public BigDecimal divide (另一个BigDecimal对象，精确几位，舍入模式) : 除法

                                RoundingMode.HALF_UP : 四舍五入
                                RoundingMode.UP : 进一法
                                RoundingMode.DOWN : 去尾法

        注意: 如果使用BigDecimal运算, 出现了除不尽的情况, 就会出现异常
     */
    public static void main(String[] args) {
        BigDecimal bd1 = BigDecimal.valueOf(10.0);
        BigDecimal bd2 = BigDecimal.valueOf(3.0);

        double result1 = bd1.add(bd2).doubleValue();
        double result2 = bd2.subtract(bd2).doubleValue();
        double result3 = bd2.multiply(bd2).doubleValue();

        System.out.println(result1);
        System.out.println(result2);
        System.out.println(result3);

        double result4 = bd1.divide(bd2, 2, RoundingMode.HALF_UP).doubleValue();
        System.out.println(result4);
    }
}

```

# Arrays 类
数组操作工具类，专门用于操作数组元素

```java
import java.util.Arrays;
import java.util.Comparator;

public class ArraysDemo {
    /*
        Arrays 数组操作工具类, 专门用于操作数组元素

        public static String toString(类型[] a)                将数组元素拼接为带有格式的字符串
        public static boolean equals(类型[] a, 类型[] b)        比较两个数组内容是否相同 (元素, 个数, 顺序)
        public static int binarySearch(int[] a, int key)       查找元素在数组中的索引 (二分查找法)
                                                                        - 注意: 操作的数组, 必须是排好顺序.
        public static void sort(类型[] a)                       对数组进行默认升序排序
     */

    public static void main(String[] args) {
        int[] arr1 = {11, 22, 33, 44, 55};
        int[] arr2 = {11, 22, 33, 44, 66};

        // 将数组元素拼接为带有格式的字符串
        System.out.println(Arrays.toString(arr1));

        // 比较两个数组内容是否相同
        System.out.println(Arrays.equals(arr1, arr2));

        // 查找元素在数组中的位置（二分查找）
        Integer[] arr = {22, 11, 66, 77, 44, 55};
        Arrays.sort(arr);
        System.out.println(Arrays.toString(arr));

        Arrays.sort(arr, new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                return o2 - o1;
            }
        });
        System.out.println(Arrays.toString(arr));
    }
}

```

# Date 类
<img src="https://cdn.nlark.com/yuque/0/2026/png/35081558/1774616709791-a73168ab-78a3-487e-bb35-de6f92612a5b.png" width="858" title="" crop="0,0,1,1" id="u23b2508f" class="ne-image">



构造方法、常见方法：

```java
package time;

import java.util.Date;

public class DateDemo {
    /*
         Date类 : 表示时间的类

            1. 构造方法 :

                public Date() : 将当前时间, 封装为Date日期对象
                public Date(long time) : 把时间毫秒值转换成Date日期对象

            2. 常见方法 :

                public long getTime() : 返回从1970年1月1日 00:00:00走到此刻的总的毫秒数
                public void setTime(long time) : 设置日期对象的时间为当前时间毫秒值对应的时间

     */
    public static void main(String[] args) {
        Date d1 = new Date();
        System.out.println(d1);

        Date d2 = new Date();
        d2.setTime(5000);  // 在 1970东八区 基础上 加5s
        System.out.println(d2);

        System.out.println(d1.getTime());
        System.out.println(d2.getTime());
    }
}

```

# SimpleDateFormat 类
用于日期格式化

+ 可以把日期对象格式化成我们想要的形式
+ 可以把字符串的时间时间形式解析成 Date 日期对象

```java
package time;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class SimpleDateFormatDemo {
    /*
        SimpleDateFormat类 : 用于日期格式化

        1. 构造方法 :

                public SimpleDateFormat() : 创建一个日期格式化对象, 使用 [默认模式]
                public SimpleDateFormat(String pattern) : 创建一个日期格式化对象, [手动指定模式]

        2. 常用方法 :

                public final String format(Date date) : 将日期对象, 转换为字符串
                public final Date parse(String source) : 将日期字符串, 解析为日期对象

     */
    public static void main(String[] args) throws ParseException {
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日");
        Date now = new Date();

        // 将日期对象，转换为指定格式的字符串
        String result = sdf.format(now);
        System.out.println(result);

        String birthday = "2008年08月08日";
        Date parse = sdf.parse(birthday);
        System.out.println(parse);
    }
}

```



**JDK8 之后新增的时间 API**

+ 都是不可变对象，修改后会返回新的事件对象，不会丢失最开始的时间
+ 线程安全
+ 可以精确到毫秒、纳秒

LocalDate：年、月、日

LocalTime：时、分、秒

LocalDateTime：年、月、日时、分、秒

DateTimeFormatter：用于时间的格式化和解析

ChronoUnit：计算时间间隔的工具类

# LocalDateTime、LocalDate、LocalTime 类
LocalDate：年、月、日

LocalTime：时、分、秒

LocalDateTime：年、月、日时、分、秒



常用方法：

```java
package time;

import java.time.*;

public class LocalDateTimeDemo {
    /*
        ------------------------------------------
        LocalDate、LocalTime、LocalDateTime

        对象的创建方式:

        1. now() : 当前时间

        2. of(...) : 设置时间

        ------------------------------------------
        LocalDateTime 转换LocalDate, LocalTime

        1. toLocalDate()
        2. toLocalTime()
     */
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();
        // 年
        int year = now.getYear();
        
        // 月
        Month month = now.getMonth();
        int monthValue = now.getMonthValue();
        
        // 日
        int dayOfMonth = now.getDayOfMonth();
        
        // 星期
        DayOfWeek dayOfWeek = now.getDayOfWeek();
        int week = dayOfWeek.getValue();
        
        // 时
        int hour = now.getHour();
        
        // 分
        int minute = now.getMinute();
        
        // 秒
        int second = now.getSecond();
        
        // 纳秒
        int nano = now.getNano();
    }

    private static void method() {
        LocalDateTime now = LocalDateTime.now();
        System.out.println(now);

        LocalDate localDate = now.toLocalDate();
        LocalTime localTime = now.toLocalTime();
        System.out.println(localDate);
        System.out.println(localTime);

        LocalDateTime localDateTime = LocalDateTime.of(2008, 8, 8, 8, 8, 8);
        System.out.println(localDateTime);

        LocalDate now1 = LocalDate.now();
        LocalTime now2 = LocalTime.now();
        System.out.println(now1);
        System.out.println(now2);
    }
}

```

修改年月日时分秒的相关方法：

```java
package time;

import java.time.LocalDate;
import java.time.LocalDateTime;

public class UpdateTimeDemo {
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();
        System.out.println(now);

        // minus: 减去
        // minusYears(年), minusMonths(月), minusDays(日), minusWeeks(周), minusHours(时),
        // minusMinutes(分), minusSeconds(秒), minusNanos(纳秒)
        System.out.println("减一小时: " + now.minusHours(1));
        System.out.println("减一分钟:" +now.minusMinutes(1));
        System.out.println("减一秒钟:" +now.minusSeconds(1));
        System.out.println("减一纳秒:" +now.minusNanos(1));

        System.out.println("对比时间, 确定方法返回的都是新的实例 >>>>>> " + now);

        System.out.println("----------------");

        // plus : 加
        // plusYears(年), plusMonths(月), plusDays(日), plusWeeks(周), plusHours(时), plusMinutes(分), plusSeconds(秒), plusNanos(纳秒)
        System.out.println("加一小时:" + now.plusHours(1));
        System.out.println("加一分钟:" + now.plusMinutes(1));
        System.out.println("加一秒钟:" + now.plusSeconds(1));
        System.out.println("加一纳秒:" + now.plusNanos(1));

        System.out.println("---------------");

        // with : 这里体现出的是,设置效果
        System.out.println("修改的效果:");
        //withYear(年), withMonth(月), withDayOfMonth(日), withHour(时), withMinute(分), withSecond(秒), withNano(纳秒)
        System.out.println(now.withYear(2008));
        System.out.println(now.withMonth(8));
        System.out.println(now.withDayOfMonth(8));
        System.out.println(now.withHour(8));
        System.out.println(now.withMinute(8));
        System.out.println(now.withSecond(8));
        System.out.println(now.withNano(8));
        System.out.println("---------------");

        LocalDate myDate = LocalDate.of(2008, 8, 8);
        LocalDate nowDate = LocalDate.now();

        //2008-08-08是否在nowDate之前?
        System.out.println(myDate + "是否在" + nowDate + "之前? " + myDate.isBefore(nowDate));

        //2008-08-08是否在nowDate之后?
        System.out.println(myDate + "是否在" + nowDate + "之后? " + myDate.isAfter(nowDate));
        System.out.println("---------------------------");

        // 判断两个时间是否相同
        System.out.println(myDate.equals(nowDate));
    }
}

```

# DateTimeFormatter 类
用于时间的格式化和解析

```java
package time;

import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class DateTimeFormatterDemo {
    /*
        用于时间的格式化和解析:

        1. 对象的获取 :

                static DateTimeFormatter ofPattern(格式) : 获取格式对象

        2. 格式化 :

                String format(时间对象) : 按照指定方式格式化

        3. 解析 :

                LocalDateTime.parse("解析字符串", 格式化对象);
                LocalDate.parse("解析字符串", 格式化对象);
                LocalTime.parse("解析字符串", 格式化对象);

     */
    public static void main(String[] args) {
        LocalDateTime now = LocalDateTime.now();
        System.out.println("格式化之前: " + now);

        // 获取格式化对象
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy年M月d日");
        // 格式化
        String result = formatter.format(now);
        System.out.println(result);

        // 解析
        String time = "2008年12月12日";
        LocalDate parse = LocalDate.parse(time, formatter);
        System.out.println(parse);
    }
}

```

# ChronoUnit 类
计算时间间隔的工具类

Duration：用于计算两个时间间隔（秒，纳秒）

Period：用于计算两个日期间隔（年月日）

ChronoUnit：用于计算两个日期间隔

```java
package time;

import java.time.LocalDateTime;
import java.time.temporal.ChronoUnit;

/**
 * ChronoUnit可用于在单个时间单位内测量一段时间，这个工具类是最全的了，可以用于比较所有的时间单位
 */
public class ChronoUnitDemo {
    public static void main(String[] args) {
        // 本地日期时间对象：此刻的
        LocalDateTime today = LocalDateTime.now();
        System.out.println(today);

        // 生日时间
        LocalDateTime birthDate = LocalDateTime.of(2028, 8, 7,
                0, 0, 0);
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
    }
}

```

> 用到了再查呗~
>

## 案例
```java
package time;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.time.LocalDate;
import java.time.format.DateTimeFormatter;
import java.time.temporal.ChronoUnit;
import java.util.Date;
import java.util.Scanner;

public class CalculateAgeTest {
    /*
        需求: 键盘录入用户的生日, 计算出用户的年龄.
     */
    public static void main(String[] args) throws ParseException {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入你的生日: ");
        String birthday = sc.next();

        // 创建时间格式化对象
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy年M月d日");
        LocalDate birthdayDate = LocalDate.parse(birthday, formatter);

        // 计算时间间隔
        long age = ChronoUnit.YEARS.between(birthdayDate, LocalDate.now());
        System.out.println(age);
    }

    private static void mathod() throws ParseException {
        Scanner sc = new Scanner(System.in);
        System.out.println("请输入你的生日: ");
        String birthday = sc.next();

        SimpleDateFormat sdf = new SimpleDateFormat("yyyy年MM月dd日");
        // 1、将用户的生日，解析为事件对象
        Date birthdayDate = sdf.parse(birthday);
        // 2、获取此刻时间
        Date now = new Date();
        // 3、计算时间差
        long time = now.getTime() - birthdayDate.getTime();
        // 4、转换单位
        System.out.println(time / 1000 / 60 / 60 / 24 / 365);
    }
}

```


