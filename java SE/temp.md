# Java 接口

>在王者里，英雄造成的伤害有两种，一种是进行物理伤害，一种是魔法伤害
这时候，就可以使用接口来实现这个效果。
接口就像是一种约定，我们约定某些英雄是物理系英雄，那么他们就一定能够进行物理攻击。

抽象类是从多个类中抽象出来的模板，如果将这种抽象进行的更彻底，则可以提炼出一种更加特殊的“抽象类”——接口（Interface）。接口是 Java 中最重要的概念之一，它可以被理解为**一种特殊的类**，但事实上它不是类。

编写接口的方式和类很相似，但是它们属于不同的概念。类描述对象的属性和方法。接口则包含类要实现的方法的声明或者是全局常量。

除非实现接口的类是抽象类，否则该类要定义接口中的所有方法。

**一个类通过继承接口的方式，从而来继承接口的抽象方法。**

**接口无法被实例化，但是可以被实现**。

**一个实现接口的类，必须实现接口内所描述的所有方法，否则就必须声明为抽象类。**

另外，在 Java 中，接口类型可用来声明一个变量，他们可以成为一个空指针，或是被绑定在一个以此接口实现的对象。

Java 接口的定义方式与类基本相同，不过接口定义使用的关键字是 interface，接口定义的语法格式如下：

```
[public] interface interface_name [extends interface1_name[, interface2_name,…]] {
    // 接口体，其中可以包含定义常量和声明方法
    [public] [static] [final] type constant_name = value;    // 定义常量
    [public] [abstract] returnType method_name(parameter_list);    // 声明方法
}
```

对以上语法的说明如下：
- public 表示接口的修饰符，当没有修饰符时，则使用默认的修饰符，此时该接口的访问权限仅局限于所属的包；
- extends 表示接口的继承关系；
- interface1_name 表示要继承的接口名称；
- constant_name 表示变量名称，一般是 static 和 final 型的；
- returnType 表示方法的返回值类型；
- parameter_list 表示参数列表，在接口中的方法是没有方法体的。


接口有以下特性：
- 接口是隐式抽象的，当声明一个接口的时候，不必使用abstract关键字。
- 接口中每一个方法也是隐式抽象的，声明时同样不需要abstract关键子。
- 接口中的方法都是公有的。


**一个具体的接口**

```
interface Animal {

   public void eat();
   public void travel();
}
```

## 接口的实现

当类实现接口的时候，类要实现接口中所有的方法。否则，类必须声明为抽象的类。

类使用implements关键字实现接口。在类声明中，Implements关键字放在class声明后面。

实现一个接口的语法，可以使用这个公式：

```
... implements 接口名称[, 其他接口, 其他接口..., ...] ...

```

```
public class MammalInt implements Animal{

   public void eat(){
      System.out.println("Mammal eats");
   }

   public void travel(){
      System.out.println("Mammal travels");
   } 

   public int noOfLegs(){
      return 0;
   }

   public static void main(String args[]){
      MammalInt m = new MammalInt();
      m.eat();
      m.travel();
   }
} 
```
运行结果

~~~
Mammal eats
Mammal travels
~~~


**重写接口中声明的方法时，需要注意以下规则**：

- 类在实现接口的方法时，不能抛出强制性异常，只能在接口中，或者继承接口的抽象类中抛出该强制性异常。
- 类在重写方法时要保持一致的方法名，并且应该保持相同或者相兼容的返回值类型。
- 如果实现接口的类是抽象类，那么就没必要实现该接口的方法。

在实现接口的时候，也要注意一些规则：

- 一个类可以同时实现多个接口。
- 一个类只能继承一个类，但是能实现多个接口。
- 一个接口能继承另一个接口，这和类之间的继承比较相似。

## 接口的继承

一个接口能继承另一个接口，和类之间的继承方式比较相似。接口的继承使用extends关键字，子接口继承父接口的方法。


下面的Sports接口被Hockey和Football接口继承：

```
public interface Sports
{
   public void setHomeTeam(String name);
   public void setVisitingTeam(String name);
}

// 文件名: Football.java
public interface Football extends Sports
{
   public void homeTeamScored(int points);
   public void visitingTeamScored(int points);
   public void endOfQuarter(int quarter);
}

// 文件名: Hockey.java
public interface Hockey extends Sports
{
   public void homeGoalScored();
   public void visitingGoalScored();
   public void endOfPeriod(int period);
   public void overtimePeriod(int ot);
}
```

## 接口的多重继承

在Java中，类的多重继承是不合法，但接口允许多重继承。

在接口的多重继承中extends关键字只需要使用一次，在其后跟着继承接口。 如下所示：

`public interface Hockey extends Sports, Event`

以上的程序片段是合法定义的子接口，与类不同的是，接口允许多重继承，而 Sports及 Event 可能定义或是继承相同的方法

## 标记接口

最常用的继承接口是没有包含任何方法的接口。

标识接口是没有任何方法和属性的接口.它仅仅表明它的类属于一个特定的类型,供其他代码来测试允许做一些事情。

标识接口作用：简单形象的说就是给某个对象打个标（盖个戳），使对象拥有某个或某些特权。

例如：`java.awt.event`包中的`MouseListener`接口继承的`java.util.EventListener`接口定义如下：
```
package java.util;
public interface EventListener
{}
```
没有任何方法的接口被称为标记接口。标记接口主要用于以下两种目的：

**建立一个公共的父接口：**
正如EventListener接口，这是由几十个其他接口扩展的Java API，你可以使用一个标记接口来建立一组接口的父接口。例如：当一个接口继承了EventListener接口，Java虚拟机(JVM)就知道该接口将要被用于一个事件的代理方案。

**向一个类添加数据类型：**
这种情况是标记接口最初的目的，实现标记接口的类不需要定义任何接口方法(因为标记接口根本就没有方法)，但是该类通过多态性变成一个接口类型。


