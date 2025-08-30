# ACM模式

## 一行输入

```java

import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        // 核心逻辑

        // 输出
        System.out.println();

        sc.close();
    }
}

```

----

## 多行输入——每行多个数据

```java

import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);

        while(sc.hasNext()){
            int a = sc.nextInt();
            int b = sc.nextInt();
        }
        

        // 核心逻辑

        // 输出
        System.out.println();

        sc.close();
    }
}

```

----

## 多行输入——第一行总数n，后面n行对应数据

```java

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        while (scanner.hasNext()) {
            int n = scanner.nextInt();

            while (n-- > 0) {
                int a = scanner.nextInt();
                int b = scanner.nextInt();
            }

        }

        // 核心逻辑

        // 输出
        System.out.println();

        sc.close();

    }
}

```

----

## 一行输入——字符之间使用空格间隔

```java

import java.util.*;

public class Main{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        
        
        String line = sc.nextLine(); // 接收⼀整⾏字符串作为输⼊
        String[] items = line.split(" "); // 字符串分割成数组

        for (String item : items) { // 遍历数组

        }

        // 核心逻辑

        // 输出
        System.out.println();

        sc.close();
    }
}

```