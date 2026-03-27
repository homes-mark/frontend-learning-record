# File 介绍
File 类代表操作系统的文件对象（文件、文件夹）

## 类创建对象
```java
import java.io.File;
import java.io.IOException;

public class FileDemo1 {
    /*
        File类的常用构造方法

            public File(String pathname)               根据文件路径创建文件对象
            public File(String parent, String child)   根据父路径名字符串和子路径名字符串创建文件对象
            public File(File  parent, String child)    根据父路径对应文件对象和子路径名字符串创建文件对象
     */
    public static void main(String[] args) throws IOException {
        File f1 = new File("D:\\A.txt");
        System.out.println(f1.exists());

        File f2 = new File("E:\\A");
        System.out.println(f2.exists());

        File f3 = new File("E:\\", "A");
        System.out.println(f2.exists());

        File f4 = new File(new File("E:\\"), "A");
        System.out.println(f4.exists());

        File f5 = new File("D:\\B.txt");
        f5.createNewFile();  // 创建文件

    }
}

```

+ File 封装的对象仅仅是一个路径名，这个路径可以是存在的，也可以是不存在的

## 相对路径和绝对路径
绝对路径：从盘符根目录开始，一直到某个具体的文件或文件夹

相对路径：相对于当前项目

```java
import java.io.File;
import java.io.IOException;

public class FileDemo2 {
    /*
        绝对路径: 从盘符根目录开始，一直到某个具体的文件或文件夹
                        E:\\A.txt
                        E:\\Develop

        相对路径: 相对于当前项目
     */
    public static void main(String[] args) throws IOException {
        File f1 = new File("A.txt");
        f1.createNewFile();

        File f2 = new File("");
        System.out.println(f2.getAbsoluteFile());

        File f3 = new File("day10\\A.txt");
        f3.createNewFile();
    }
}

```

# File 类的常用 API
## File 类的判断方法
```java
import java.io.File;

public class FileDemo3 {
    /*
        File类的判断相关方法

            public boolean isDirectory()    判断此路径名表示的File是否为文件夹
            public boolean isFile()         判断此路径名表示的File是否为文件
            public boolean exists()         判断此路径名表示的File是否存在
     */
    public static void main(String[] args) {
        File f = new File("day10\\A.txt");

        System.out.println(f.isDirectory());
        System.out.println(f.isFile());
        System.out.println(f.exists());
    }
}

```

## 键盘录入文件夹路径
```java
import java.io.File;
import java.util.Scanner;

public class FileTest1 {
    /*
        需求: 键盘录入一个文件夹路径，如果输入错误就给出提示，并继续录入，直到正确为止

        分析:
            1. 输入的路径有可能不存在
            2. 输入的路径有可能是文件路径

            封装为File对象
                调用 exists() 判断是否存在
                调用 isFile() 判断是否是文件

     */
    public static void main(String[] args) {
        File dir = getDir();
        System.out.println(dir);
    }

    private static File getDir() {
        Scanner sc = new Scanner(System.in);
        while (true) {
            System.out.println("请输入一个文件夹路径: ");
            String dir = sc.next();

            File file = new File(dir);
            if (!file.exists()) {
                System.out.println("您输入的文件夹路径不存在, 请检查!");
            }else if (file.isFile()) {
                System.out.println("您输入的是一个文件路径, 请重新输入文件夹路径: ");
            }else {
                return file;
            }
        }
    }

}

```

## File 类的常用方法
```java
import java.io.File;
import java.util.Date;

public class FileDemo4 {
    /*
        File类常用方法:

        public long length()                返回文件的大小（字节数量）
                                                    注意: 如果是文件夹对象, 调用该方法, 返回的结果是错误的.
        public String getAbsolutePath()     返回文件的绝对路径
        public String getPath()             返回定义文件时使用的路径
        public String getName()             返回文件的名称，带后缀
        public long lastModified()          返回文件的最后修改时间（时间毫秒值）
     */
    public static void main(String[] args) {
        File f = new File("A.txt");
        System.out.println(f.length());

        File f2 = new File("day10\\A.txt");
        System.out.println(f2.getAbsoluteFile());

        System.out.println(f.getPath());
        System.out.println(f2.getPath());
        System.out.println(f2.getName());

        long time = f.lastModified();
        System.out.println(time);

        Date d = new Date(time);
        System.out.println(d);
    }
}

```

```java
import java.io.File;
import java.io.IOException;

public class FileDemo5 {
    /*
        File类常用方法: 创建和删除

            public boolean createNewFile()      创建一个新的空的文件
            public boolean mkdir()              只能创建一级文件夹
            public boolean mkdirs()             可以创建多级文件夹
            public boolean delete()             删除由此抽象路径名表示的文件或空文件夹
     */
    public static void main(String[] args) throws IOException {
        File f1 = new File("day10\\B.txt");
        System.out.println(f1.createNewFile());

        File f2 = new File("day10\\aaa");
        System.out.println(f2.mkdirs());

        System.out.println(f1.delete());
        System.out.println(f2.delete());
    }
}

```

File 类的遍历方法：

```java
import java.io.File;

public class FileTest2 {
    /*
        需求：键盘录入一个文件夹路径，找出这个文件夹下所有的 .java 文件

        public File[] listFiles()  获取当前目录下所有的  “一级文件对象”  返回 File 数组
     */
    public static void main(String[] args) {
        File dir = FileTest1.getDir();
        printJavaFile(dir);
    }

    public static void printJavaFile(File dir) {
        // 1、获取当前文件夹下所有的文件和文件夹对象
        File[] files = dir.listFiles();
        // 2、遍历数组，获取每一个文件和文件夹对象
        for (File file : files) {
            // 3、判断当前对象是否是文件，并且是java文件
            if (file.isFile() && file.getName().endsWith(".java")) {
                System.out.println(file);
            }
        }
    }
}
```

listFiles() 方法注意事项：

+ 当调用者File表示的<font style="color:#DF2A3F;">路径不存在</font>时，返回null
+ 当调用者File表示的<font style="color:#DF2A3F;">路径是文件</font>时，返回null
+ 当调用者File表示的路径是一个<font style="color:#DF2A3F;">空文件夹</font>时，返回一个<font style="color:#DF2A3F;">长度为0的数组</font>
+ 当调用者File表示的路径是<font style="color:#DF2A3F;">需要权限才能访问</font>的文件夹时，返回nulI

# 递归介绍
方法直接或者间接调用本身

递归的思路：将大问题，层层转化为一个与原问题，相似的，规模更小的问题来解决

+ 递归如果没有控制好终止，会出现递归死循环，导致栈内存溢出现象

```java
public class RecursionDemo1 {
    /*
    * 求 5的阶乘   5!
    * */
    public static void main(String[] args) {
        int result = jc(5);
        System.out.println(result);
    }

    public static int jc(int num) {
        if (num == 1) {
            return 1;
        } else {
            return num * jc(num - 1);
        }
    }
}
```

```java
public class RecursionDemo2 {
    /**
     * 斐波那契数列: 1 1 2 3 5 .....
     */
    public static void main(String[] args) {
        System.out.println(get(20));
    }

    public static int get(int month) {
        // 前两个月兔子的对数为1对
        if (month == 1 || month == 2) {
            return 1;
        } else {
            return get(month - 1) + get(month - 2);
        }
    }
}

```

# 递归案例
```java
import java.io.File;

public class FileTest3 {
    /*
       需求：键盘录入一个文件夹路径，找出这个文件夹下所有的 .java 文件 (考虑子文件夹)

     */
    public static void main(String[] args) {
        File dir = FileTest1.getDir();
        printJavaFile(dir);
    }

    public static void printJavaFile(File dir) {
        // 1、获取当前文件夹下所有的文件和文件夹对象
        File[] files = dir.listFiles();
        // 2、遍历数组，获取每一个文件和文件夹对象
        for (File file : files) {
            // 3、判断当前对象是否是文件，并且是java文件
            if (file.isFile() && file.getName().endsWith(".java")) {
                System.out.println(file);
            } else if (file.isDirectory()) {
                // 如果是文件夹，进入这个文件夹，继续查找 java文件
                // 递归进入
                if (file.listFiles() != null) {
                    printJavaFile(file);
                }
            }
        }
    }
}

```

```java
import java.io.File;

public class FileTest4 {
    /*
        需求 : 设计一个方法, 删除文件夹
        注意 : delete() 只能删除空文件夹
     */
    public static void main(String[] args) {
        File dir = new File("G:\\test");
        deleteDir(dir);
    }

    private static void deleteDir(File dir) {
        File[] files = dir.listFiles();
        for (File file : files) {
            if (file.isFile()) {
                file.delete();
            } else {
                if (file.listFiles() != null) {
                    deleteDir(file);
                }
            }
        }
        dir.delete();
    }
}
```

```java
import java.io.File;

public class FileTest5 {
    /*
        需求: 键盘录入一个文件夹路径，统计文件夹的大小
     */
    public static void main(String[] args) {
        File dir = FileTest1.getDir();

        long length = getDirLength(dir);
        System.out.println("字节数量为: " + length);
    }

    private static long getDirLength(File dir) {
        long result = 0;
        File[] files = dir.listFiles();
        for (File file : files) {
            if (file.isFile()) {
                result += file.length();
            } else {
                if (file.listFiles() != null) {
                    result += getDirLength(file);
                }
            }
        }
        return result;
    }
}

```
