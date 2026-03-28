# Java-Study-Notes-0319
3月19日Java学习笔记
# 结构化编程实践

实验目的：学会Java各种选择结构，包括if ~ else结构和switch结构；学会Java各种循环结构的使用，包括while循环、do ~ while循环和for循环以及循环结构的嵌套。

## 【题目1】

输入三角形的三边长，输出三角形的面积。利用公式 

计算三角形的面积，其中s=(a+b+c)/2。

![](https://img2024.cnblogs.com/blog/2979549/202603/2979549-20260328222511404-2137222114.png)

调用Math.sqrt(x)：计算x的平方根。

代码：

```java
import java.util.Scanner;

public class Problem1
{
    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);
        double a,b,c,p,s;
        System.out.println("请输入三角形的三边长");
        a=sc.nextDouble();
        b=sc.nextDouble();
        c=sc.nextDouble();
        if(a+b<=c||a+c<=b||b+c<=a)
        {
            System.out.println("无法构成三角形，请输入合理参数！");
        }
        else
        {
            p=(a+b+c)/2.0;
            s=Math.sqrt(p*(p-a)*(p-b)*(p-c));
            System.out.println("三角形的面积为"+s);
        }
    }
}
```

运行截图：

![](https://img2024.cnblogs.com/blog/2979549/202603/2979549-20260328222514626-519661159.png)

## 【题目2】

编写java程序从键盘输入一个年份和一个月份，获得该月的天数。

例如：

输入年份：2000

输入月份：2

输出：2000年2月份有29天。

代码：

```java
import java.util.Scanner;

public class Problem2
{
    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);
        int y,m;
        boolean run;
        System.out.print("请输入年份:");
        y=sc.nextInt();
        System.out.print("请输入月份:");
        m=sc.nextInt();
        if(y%4==0&&y%100!=0||y%400==0) run=true;
        else run=false;
        System.out.print(y+"年"+m+"月份有");
        switch(m)
        {
            case 1,3,5,7,8,10,12-> System.out.print("31");
            case 2->
            {
                if(run) System.out.print("29");
                else System.out.print("28");
            }
            case 4,6,9,11-> System.out.print("30");
        }
        System.out.println("天。");
    }
}
```

写法2：

```java
import java.util.Scanner;

public class Problem2Method2
{
    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);
        int y,m,d;
        boolean run;
        System.out.print("请输入年份:");
        y=sc.nextInt();
        System.out.print("请输入月份:");
        m=sc.nextInt();
        if(y%4==0&&y%100!=0||y%400==0) run=true;
        else run=false;
        d=switch(m)
        {
            case 1,3,5,7,8,10,12->31;
            case 2->
            {
                if(run) yield 29;
                else yield 28;
            }
            case 4,6,9,11->30;
            default->0;
        };
        System.out.print(y+"年"+m+"月份有"+d+"天。");
    }
}
```

运行截图：

![](https://img2024.cnblogs.com/blog/2979549/202603/2979549-20260328222517553-73038058.png)

## 【题目3】

编写程序，计算并输出1-1000之间素数之和及个数。

代码：

```java
public class Problem3
{
    public static void main(String[] args)
    {
        var isPrime=new boolean[1005];
        for(int i=0;i<1005;i++) isPrime[i]=true;
        int cnt=0,sum=0;
        isPrime[0]=isPrime[1]=false;
        for(int i=2;i*i<=1000;i++)
        {
            if(isPrime[i])
            {
                for(int j=i*i;j<=1000;j+=i)
                {
                    isPrime[j]=false;
                }
            }
        }
        System.out.println("1-1000中的素数有：");
        for(int i=1;i<=1000;i++)
        {
            if(isPrime[i])
            {
                System.out.print(i+" ");
                cnt++;
                if(cnt%10==0) System.out.println();
                sum+=i;
            }
        }
        System.out.println();
        System.out.println("共有"+cnt+"个，和为"+sum);
    }
}
```

运行截图：

![](https://img2024.cnblogs.com/blog/2979549/202603/2979549-20260328222521167-690421829.png)

## 【题目4】

由计算机随机产生一个1~30之间的整数magic，让用户来猜，最多给5次机会，程序显示是否猜中的消息，若用户输入的数比magic小，提示用户“很遗憾，您猜小了！”；若比magic大，提示用户“很遗憾，您猜大了！”；若猜对了，显示“恭喜，答对！”程序结束。若5次机会后还没猜对，显示“失败，游戏结束！” 。

代码：

```java
import java.util.*;
public class Problem4
{
    public static void main(String[] args)
    {
        Scanner sc=new Scanner(System.in);
        Random rand=new Random();
        int magic=rand.nextInt(30)+1;
        int in,cnt=1;
        System.out.println("随机生成了一个1~30之间整数，请你来猜猜它");
        in=sc.nextInt();
        while(true)
        {
            if(in==magic)
            {
                System.out.println("恭喜，答对！");
                break;
            }
            else if(in<magic)
            {
                System.out.println("很遗憾，您猜小了！");
            }
            else if(in>magic)
            {
                System.out.println("很遗憾，您猜大了！");
            }
            cnt++;
            if(cnt>5)
            {
                System.out.println("失败，游戏结束！这个数是"+magic);
            }
            in=sc.nextInt();
        }
    }
}
```

运行截图：

![](https://img2024.cnblogs.com/blog/2979549/202603/2979549-20260328222524024-1023392970.png)

## 三、心得体会与总结

第一题使用double类型存储变量，再根据海伦公式计算三角形面积。经老师提醒，又加了一个判断输入的三边是否能构成三角形的语句（判断规则：任意两边之和大于第三边），增加了程序的健壮性。

第二题需先判断输入的年份是平年还是闰年，因为这决定了该年的2月有28天还是29天，我用了一个boolean类型的变量来记录。之后用switch~case来根据输入的月份输出天数，我给出了两种写法，分别是switch语句和switch表达式。

第三题我使用埃氏筛算法，筛去所有的合数，剩下的便都是素数。实现方法为新建一个boolean类型的数组，全体元素初始化为true，将既不是素数也不是合数的数（0和1）与合数（素数2、3、5、7...的i（i>=2）倍）筛去，赋值为false，剩下仍为true的便是素数。时间复杂度O(nloglogn)

第四题用rand.nextInt()函数生成一个随机数，再使用循环结构让用户不断输入一个数来猜数，根据输入的数大于、小于、等于该随机数作出输出反馈。若猜的次数大于5，则猜数失败，并告诉用户正确答案。

Random类使用方法：

Random rand = new Random();

Int randomNum = rand.nextInt((max-min)+1)+min;

max是上限，min是下限。
