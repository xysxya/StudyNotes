# ***继承的理解以及堆空间情况***

- 子类继承父类后，子类至少存在一个构造函数存在super()结构，且这个构造函数必被调用。也就是说，子类一旦创建，那么其父类中的结构也一定会随之加载。

- 可以将子类与父类的继承关系理解为两个集合，其中父类是子类的真子集

- 小集合中为父类的所有结构

- 大集合中，若没有方法的重写，则大集合(子类) 中有着与小集合(父类) 中一模一样的结构，除此之外，大集合中还有一些自己独特的结构


## 对于属性和方法，继承情况不同。

一般情况下，如果子类中定义了于父类同名的属性，可以类比方法的重写。但是，但是，但是，如果发生了多态，父类引用调用的方法是子类重写后的方法，但父类引用调用的属性仍然是父类的属性，这就是所谓的多态性不适用于属性。



# *方法的重写 overwirte/override*

- 方法的重写(区别于方法的重载)

- 重写：子类继承父类以后，可以对父类中同名同参数的方法进行覆盖操作

- 重写以后，当创建子类对象以后，通过子类对象调用子父类中的同名参数的方法时，实际执行的是子类重写父类的方法

  

- 重写的规定：

- 子类重写的方法的方法名和形参列表与父类被重写的方法的方法名和形参列表相同

- 子类重写的方法的权限修饰符不小于父类被重写的方法的权限修饰符

- 特别的，子类不能重写父类中声明为private权限的方法(即使写了，也相当于子类重新定义了一个方法)

  

- 返回值类型:

- 父类被重写的方法的返回值类型是void，则子类重写的方法返回值类型只能是void

- 父类被重写的方法的返回值类型是A类型，则子类重写的方法的返回值类型可以是A类或A类的子类

- 父类被重写的方法的返回值类型是基本数据类型，则子类重写的方法的返回值类型必须是相同的基本数据类型

  

- 子类重写的方法抛出的异常类型不大于父类被重写的方法抛出的异常类型

- 子类和父类中同名同参数的方法要么都声明为非static(是重写),要么都声明为static(不是重写)




# ***多态性***

- 可以理解为一个事物的多种形态

- 多态性:父类的引用指向子类的对象(子类的对象初始化父类的引用)

- 多态的使用：虚拟方法调用。当调用子父类同名同参数的方法时，实际执行的是子类重写父类的方法-----虚拟方法调用
  有了对象的多态性以后，内存中实际上是加载了子类所特有的属性和方法，但是由于变量声明为父类类型，
  导致编译时，只能调用父类中声明的属性和方法。子类特有的属性和方法不能调用
- 有了对象的多态性以后，在编译期，只能调用父类中声明的方法，但是在运行期间，实际执行的是子类重写父类的方法(  编译看左边，运行看右边   Person p1=new Man()  )

- 使用前提：要有类的继承关系

- 方法的重写

- 对象的多态性，只适用于方法，不适用于属性(即属性编译运行都看左边  就近原则)

- 多态是一种运行时行为

- 多态要与方法的重写连用，否则是没有意义的，因为父类的引用无法访问子类特有的结构


************************************************************************

## 向下转型（instanceof）

向下转型必须建立在已经产生多态的基础上的，否则是没有意义的

正是因为发生多态时，父类无法访问子类特有的结构，才需要向下类型转换

| 类           | 向下转型     | 向上转型(多态) |
| ------------ | ------------ | -------------- |
| 基本数据类型 | 强制类型转换 | 自动类型提升   |

a instanceof A 其中， a是实例对象，A是类

注意！instancof运算符有使用条件！！！

instanceof用来使用条件是对象a与类A必须存在子父类关系，如果对象a是类A或A的子类的实例，则返回true。如果对象a是类A的父类(直接或间接)的实例，则返回false。如果对象a与类A毫无关系，则编译报错

总结：实例对象<=类，返回true

​			实例对象>类，返回false

​			实例对象与类无子父类关系，编译报错



```java
	Person p2=new Man();
    //如何才能调用子类特有的属性和方法？
	//使用强制类型转换符(向下转型)
	Man m1=(Man)p2;
	m1.earnMoney();
	m1.isSmoking=true;
	
	//使用强转时，可能会出现ClassCaseException的异常
	Woman w1=(Woman)p2;
	w1.goShopping();
	
	//instanceof的使用
	 /* a instanceof A:判断对象a是否是类a 的实例，如果是，返回true,如果不是,返回false
	 * 为了避免在向下转型时出现ClassCastException异常，在向下转型之前，先进行instanceof 判断
	 * 如果是true 则进行向下转型 如果是false 则不进行向下转型 
	 * 若 a instanceof A 返回 true, B是A的父类
	 * 则 a instanceof B 返回 true
	 */
```



# 方法的重写与多态性的联系

- 多态性是指父类的引用能够被子类初始化，即父类引用能指向子类对象。

- 但是，即使发生了多态，此时父类引用仍然不能访问子类中特有的结构，只能访问父类与子类共有的结构，即子类所继承的结构。所以，子类一般要重写父类中的方法，进而达到重写与多态性联用的目的，否则多态是没有任何意义的。

- 为了使得父类引用能够访问到子类特有的结构，引入了向下转型，即将父类引用强制转换为子类引用，进而使得能够访问子类特有结构。为避免在向下转型时出现ClassCastException异常，引入了 instanceof 关键字用来判断对象a是否是类A的实例(a instanceof A),返回值为布尔类型




# ==运算符与equals()区别

## 1.  ==  运算符

- 基本数据类型：比较两个基本数据类型是否相等（类型不一定要相同，boolean除外）

- 引用数据类型：比较两个对象的地址值是否相同，即两个引用是否指向同一个对象实体

- 特别的，对于String类型，如果是通过 String str1="abc";  String str2="abc";  的方式声明。那么，str1==str2的结果为true

- 因为String 类型并非在堆空间开辟内存，而是在字符串常量池中开辟，常量池会将字符串相同的String 类型安排在同一地址，也就是说==运算符虽然比较的仍然是是否是同一地址，但是字符串常量池的特性辅助其增加了判断两个String 类型是否相同的能力。

- 注意 如果String 类型是通过 String str1=new String ("abc");  String str2=new String ("abc");  的方式声明，那么，str1==str2的结果为false。


## 2.equals()方法

equals()是Object类的一个方法，而非运算符，所以只适用于引用数据类型

Object类中equals()方法的定义：

```java
public boolean equals(Object obj) {
        return (this == obj);
    }
```

Object类中定义的方法和==运算符作用是相同的，比较两个对象的地址值是否相同，即比较两个引用是否指向同一个对象实体

但是，String、Date、File、包装类等都重写了Object类中了equals()方法。重写以后，比较的不是两个引用的地址是否相同，而是比较两个对象的“实体内容”是否相同。

String 重写equals()方法：

```Java
public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        if (anObject instanceof String) {//判断anObject是否是String的直接或间接子类
            
            //在编译期间，anObject是Object类的对象，所以，不能通过多态将anObject转换成String类型，虽然通过了instanceof 验证其是String 的子类，但是多态是运行时行为，在编译期间无效，所以，要通过强制类型转换将anObject转换为String 类型，即父类强制转换为子类
            String anotherString = (String)anObject;
            int n = value.length;
            if (n == anotherString.value.length) {
                char v1[] = value;
                char v2[] = anotherString.value;
                int i = 0;
                while (n-- != 0) {
                    if (v1[i] != v2[i])
                        return false;
                    i++;
                }
                return true;
            }
        }
        return false;
    }
```



自定义Person类equals()方法的重写：

```java
@Override
	public boolean equals(Object obj) {
		if(this==obj) {
			return true;
		}
		if(obj instanceof Person) {
			Person p=(Person)obj;
            //注意不要写成...&&this.name==p.name&&...
            //可以说，引用数据类型不会用==运算符，基本无意义
			if(this.age==p.age&&this.name.equals(p.name)&&this.id==p.id) {
				return true;
			}
		}
		return false;
	}
```

x.equals(null),永远是false

x.equals(与x不同类型的对象),永远是false





# ***toString()方法***

当输出一个对象的引用时，实际上就是调用当前对象的toString()方法，只是省略了toString()部分

```java
Person p=new Person();

//以下两句意义相同
System.out.println(p);
System.out.println(p.toString());
```

Object类中toString() 方法的定义：

```java
public String toString() {
        return getClass().getName() + "@" + Integer.toHexString(hashCode());
    }
```



String、Date、File、包装类等都重写了Object类中的toString() 方法，使得在调用对象toString() 方法时，返回实体内容



# ***包装类(Wrapper)***

Java提供了8种基本数据类型对应的包装类，使得基本数据类型变量具有类的特征。

| 基本数据类型 | 对应的包装类 |
| ------------ | ------------ |
| byte         | Byte         |
| short        | Short        |
| int          | Integer      |
| long         | Long         |
| float        | Float        |
| double       | Double       |
| boolean      | Boolean      |
| char         | Character    |

说明：除boolean、char外，其他包装类均继承于Number类

## 基本数据类型、包装类、String 类 三者之间的相互转换

### 1.基本数据类型---->包装类：调用包装类的构造函数

```java
public void test1() {
		int num1=10;
		Integer in1=new Integer(num1);
		System.out.println(in1.toString());//10
		
		Integer in2=new Integer("123");
		System.out.println(in2);//123
		
		Float f1=new Float(12.3f);
		Float f2=new Float("12.4");
		System.out.println(f1);//12.3
		System.out.println(f2);//12.4
		
		Boolean b1=new Boolean(true);
		Boolean b2=new Boolean("true");
		Boolean b3=new Boolean("true123");
		Boolean b4=new Boolean("TrUe");
		System.out.println(b1);//true
		System.out.println(b2);//true
		System.out.println(b3);//false
		System.out.println(b4);//true
	}
```

### 2.包装类---->基本数据类型：调用包装类的xxxValue()方法

```java
public void test2() {
		
		Integer in1=new Integer(12);
		int num1=in1.intValue();
		System.out.println(num1+1);
		
		Float f1=new Float(12.3);
		float num2=f1.floatValue();
		System.out.println(num2+1);
	}
```

### 3.基本数据类型---->包装类：自动装箱

###     包装类---->基本数据类型：自动拆箱

```java
	public void test3() {
		//自动装箱
		int num1=10;
		Integer in1=num1;
		boolean b1=true;
		Boolean B=b1;
		
		//自动拆箱
		int num2=in1;
		boolean b2 =B;
	}
```

### 4.基本数据类型、包装类---->String 类型

```java
public void test4() {

		//方式1：连接运算
		int num1=10;
		String str1=num1+"";
		//方式2：调用String 重载的ValueOf(xxx)
		float f1=12.3f;
		String str2=String.valueOf(f1);
		
		Double d1=new Double(12.4);
		String str3=String.valueOf(d1);
	}
```

### 5.String 类型---->基本数据类型、包装类：调用包装类的parseXxx()方法

```java
public void test5() {
		
		String str1="123";
		int num1=Integer.parseInt(str1);
		System.out.println(num1);
		
		String str2="true";
		boolean b1=Boolean.parseBoolean(str2);
		System.out.println(b1);
	}
```

## 6.总结

基本数据类型<---->包装类：			自动装箱、自动拆箱

基本数据类型、包装类---->String	String str = String.valueOf (基本数据类型、包装类)  

String---->基本数据类型、包装类	int num = Integer.parseInt (String str)

​														float num=Float.parseFloat(String str)

## 包装类的内部结构

```java
public void test7() {		
		//Integer内部定义了IntegerCache结构，IntegetCache中定义了Integer[]，
    	//保存了-128~127范围内的整数（因其高频），如果通过自动装箱的方式且给Integer复制的范围在-128~127之间时，会使用数组中的元素，不会再new新的Integer对象，提高效率
		Integer i=new Integer(1);
		Integer j=new Integer(2);
		System.out.println(i==j);//false
		
		Integer m=1;
		Integer n=1;
		System.out.println(m==n);//true
		
		Integer x=128;//超出-128~127的范围会new 一个Integer对象
		Integer y=128;
		System.out.println(x==y);//false
	}
```

# 单元测试方法

@Test

需要声明一个公有 返回值类型为void 无参的方法

public void unitTest(){

​		//方法体

}

运行时要将光标放在方法名上

# ***static关键字***

 static:静态的

static可以用来修饰：属性、方法、代码块、内部类

## 1.static修饰属性：静态变量

- 属性按是否使用static修饰，分为：静态属性和非静态属性(实例变量)

- 实例变量：创建了类的多个对象，每个对象都独立的拥有一套类中的非静态属性。当修改其中一个对象中的

  非静态属性时，不会导致其他对象中同样的属性值的修改

- 静态变量：创建了类的多个对象，多个对象共享同一个静态变量。当通过某一个对象修改静态变量时，会导致

  其他对象调用此静态变量时，是修改过了的

- static修饰属性的说明：

  静态变量随着类的加载而加载，静态变量的加载早于对象的创建，可以通过 “ 类.静态变量 ” 的方式调用

  由于类只会加载一次，则静态变量再内存中也只会加载一份：存放再方法区的静态域中


| 能否调用 | 类变量（静态变量） | 实例变量 |
| -------- | ------------------ | -------- |
| 类       | Yes                | No       |
| 对象     | Yes                | Yes      |

## 2.static修饰方法：静态方法

随着类的加载而加载：可以通过 “ 类.方法 ” 的方式调用

| 能否调用 | 类方法（静态方法） | 实例方法 |
| -------- | ------------------ | -------- |
| 类       | Yes                | No       |
| 对象     | Yes                | Yes      |

静态方法中，只能调用静态方法或静态属性

非静态方法中，既可以调用非静态的方法和属性，也可以调用静态的方法和属性

注意：在静态方法内，不能使用this、super关键字，静态结构是通过 类名.结构 的方式调用的，一般类名会被省略



# ***单例设计模式***

## 1.饿汉式

优点：线程安全

缺点：对象加载时间长（生命周期过长）

```java
public class Test {
    
	public static void main(String[] args) {
        Bank bank1=Bank.getInstance();
		Bank bank2=Bank.getInstance();
		System.out.println("bank1 & bank2 的地址值是否相同："+(bank1==bank2));//true
    }
}

class Bank{
	//步骤1：私有化类的构造器
	private Bank() {
		
	};
	
	//步骤2：类内创建类的静态私有对象
	private static Bank instance=new Bank();
	
	//步骤3：提供公共的静态方法，返回类的对象
	public static  Bank getInstance() {
		return instance;
	}
}
```

## 2.懒汉式

优点：延迟对象的创建（缩短了生命周期）

缺点：线程不安全

```java
public class Test {
    
	public static void main(String[] args) {
       Order order1=Order.getInstance();
		Order order2=Order.getInstance();
		System.out.println("order1 & order2 的地址值是否相同："+(order1==order2));
    }
}

class Order{
	//步骤1：私有化类的构造器
	private Order() {
		
	}
	//步骤2：声明当前类的静态对象，但不初始化
	private static Order instance = null;
	//声明公共静态返回当前类对象的方法
	public static Order getInstance() {
		if(instance ==null) {
			instance=new Order();
		}
		return instance;
	}
}
```

# ***main()方法***

main()方法作为程序的入口，也是一个普通的静态方法

在main()方法调用本类结构需要先造对象的原因：因为main()是静态方法，无法调用非静态结构，其实有两种方式调用类种的结构。一是创造当前类对象，通过对象调用非静态结构。二是将想要调用的属性、方法声明为静态再调用。

mian()方法的参数也可作为与系统交互的方式。



# ***代码块***

作用：初始化类、对象

代码块只能被static修饰

分类：静态代码块、非静态代码块

静态代码块的执行优先于非静态代码块的执行，非静态代码块的执行优先于构造器的执行，构造器的执行优先于方法的执行

## 1.静态代码块：

随着类的加载而执行 (区别于静态方法随着类的加载而加载)

只执行一次

只能调用静态结构

作用：初始化类的信息

## 2.非静态代码块

随着对象的创建而执行(每创建一个对象，就执行一次非静态代码块)

静态结构与非静态结构均可调用

作用：可以在创建对象时，对对象的属性进行初始化

## 3.属性赋值方法及优先级

| 优先级 | 赋值方式（同优先级调用顺序与位置有关）                       |
| ------ | ------------------------------------------------------------ |
| 1      | 默认初始化(0、null等)                                        |
| 2      | 显式初始化(int data=1)、在代码块中赋值(静态代码块优先于非静态代码块) |
| 3      | 构造器中初始化                                               |
| 4      | 通过  对象.属性 的方式赋值                                   |

## 4.继承关系下各初始化方式顺序

静态先行，由父及子

父类的静态代码块--->子类的静态代码块--->父类的非静态代码块--->父类的构造器--->子类的非静态代码块--->子类的构造器

```java
public class OOPTest {

	public static void main(String[] args) {
		 C c=new C();
	}
}
class A{
	static {
		System.out.println("爷类静态代码块调用");
	}
	{
		System.out.println("爷类非静态代码块调用");
	}
	A(){
		System.out.println("爷类构造器调用");
	}
}
class B extends A{
	static {
		System.out.println("父类静态代码块调用");
	}
	{
		System.out.println("父类非静态代码块调用");
	}
	B(){
		System.out.println("父类构造器调用");
	}
	
}
class C extends B{
	static {
		System.out.println("子类静态代码块调用");
	}
    //类C中构造器与非静态代码块书写顺序与最终输出结果无关
    C(){
		System.out.println("子类构造器调用");
	}
	{
		System.out.println("子类非静态代码块调用");
	}
}

//程序运行结果如下：
爷类静态代码块调用
父类静态代码块调用
子类静态代码块调用
    
爷类非静态代码块调用
爷类构造器调用
    
父类非静态代码块调用
父类构造器调用
    
子类非静态代码块调用
子类构造器调用
```



# ***final关键字***

final关键字：最终的

final可以修饰的结构：类、对象、方法、变量

1.final修饰类：该类不能被其他类所继承(如：String类、System类、StringBuffer类)

2.final修饰对象：表示该引用名不能再被赋值(即不能指向其他对象)

3.final修饰方法：表示该方法不能被重写

4.final修饰变量：此时“变量”成为一个常量

​		(1)final修饰属性：可以赋值的位置有：显式初始化、代码块中初始化、构造器中初始化   (注意！，被final修饰的属性在类中只能被上述三种初始化方式之一初始化，不能同时被两种或三种方式初始化)

​		(2)final修饰局部变量：尤其是使用final修饰形参时，表明此形参是一个常量，当我们调用此方法时，给常量形参赋一个	实参。一旦赋值以后，就只能在方法体内使用此形参的初始值，但不能重新赋值

static final 用来修饰属性：全局常量

# ***abstract关键字***

 abstract：抽象的

abstract可以用来修饰的结构：类、方法

## 1.abstract修饰类：抽象类

​		该类不能实例化

​		抽象类中仍有构造器，目的是使得子类对象能够被实例化

## 2.abstract修饰方法：抽象方法

只有方法的声明，没有方法体

抽象方法只能声明在抽象类中(包含抽象方法的类一定是一个抽象类) (反之，抽象类不一定要有抽象方法)

## 3.注意事项：

1.若子类重写了父类中所有的抽象方法后，该子类能够被实例化

2.若子类没有重写父类中的所有抽象方法，则此子类也是一个抽象类，需要使用abstract修饰

3.abstract不能用来修饰属性、构造器等结构

4.abstract不能用来修饰私有方法(私有方法不能被重写)、静态方法、final类、final方法

## 4.匿名类的创建

```Java
public class AbstractTest {

	public static void main(String[] args) {
        //理论上抽象类是不能被实例化的，但是如果强行实例化，则需要代码块重写抽象类中
		Person p=new Person() {
			@Override
			public void eat() {
				System.out.println("吃东西");
			}
			@Override
			public void walk() {
				System.out.println("呼吸");
			}
		};
		p.walk();
		p.eat();
	}
	}
}
abstract class Person{
	abstract public void eat();
	abstract public void walk();
}
```

# ***接口 interface***

接口的使用

1.用interface定义

2.在Java中，接口和类是并列的两个结构

3.定义接口中的成员

​		JDK7及以前：只能定义全局常量和抽象方法

​				全局常量：public static final，但是书写时可以省略不写

​				抽象方法：public abstract,但是书写时可以省略不写

​		JDK8及以后：除定义全局常量和抽象方法外，还可以定义公共静态方法(public static)、公共默认默认方法(public 								default)

 * 接口中定义的静态方法，只能通过接口来调用
 * 通过实现类的对象，可以调用接口中的默认方法
 * 如果实现类重写了接口中的默认方法，调用时，调用的是重写后的方法
 * 如果子类(实现类)的父类和实现的接口中声明了同名同参数的方法，且在子类没有重写此方法的前提下，默认调用的是父类的方法------>类优先原则    (区别于对于属性而言会报错)
 * 如果实现类实现了多个接口，而这多个接口中定义了同名同参数的方法，那么实现类如果没有重写此方法，那么编译报错。因此，必须在实现类中重写接口中同名方法

4.接口中不能定义构造器，意味着接口不可以实例化

5.接口一般通过让类去实现(implements)的方式来使用

​		如果实现类覆盖了接口中的所有抽象方法，则此实现类就可以实例化

​		如果实现没有覆盖接口中所有的抽象方法，则此实现类仍为一个抽象类

6.Java类可以实现多个接口--->弥补Java单继承性的局限性

7.类的格式： class AA extends BB implements CC,DD,EE{...}

8.接口与接口之间的关系：继承，且可以多重继承

```java
interface Flyable{
	
	//全局常量
	public static final int MAX_SPEED=7900;
	int MIN_SPEED=1;//public static final可省略
	//抽象方法
	public abstract void fly();
	void stop();//public abstract 可省略
}
interface Attackable{
	void attack();
}
class Plane implements Flyable,Attackable{
	@Override
	public void fly() {
		System.out.println("飞机可以通过引擎起飞");
	}
	@Override
	public void stop() {
		System.out.println("驾驶员减速停止");
	}
    @Override
	public void attack() {
		System.out.println("具有攻击性");
	}
}
class Bullet extends Object implements Flyable,Attackable,CC{//注意extends 与 implements书写顺序
//类中应重写所有抽象方法此类才能被实例化
}
```



## 接口也存在多态性

```java
public class USBTest {

	public static void main(String[] args) {
		Computer com=new Computer();
		Flash flash =new Flash();
		com.transferData(flash);
	}
}

class Computer{
	public void transferData(USB usb) {//USB usb=new Flash();  体现了接口也具有多态性
		usb.start();
		System.out.println("具体传输数据细节");
		usb.stop();
	}
}

interface USB {
	void start();

	void stop();
}

class Flash implements USB{

	@Override
	public void start() {
		System.out.println("U盘开始工作");
	}
	@Override
	public void stop() {
		System.out.println("U盘停止工作");
	}
	
}
//////////////////////////////////////////////////////////////////////////////////////////////////
public static void main(String[] args) {
		Computer com=new Computer();
		//创建接口的非匿名实现类的非匿名对象
		Flash flash =new Flash();
		com.transferData(flash);
    
		//创建接口的非匿名实现类的匿名对象
		com.transferData(new Printer());
    
		//创建接口的匿名实现类的非匿名对象
		USB phone=new USB() {
			@Override
			public void start() {
				System.out.println("手机开始工作");
			}
			@Override
			public void stop() {
			System.out.println("手机停止工作");	
			}
		};
		com.transferData(phone);
    
		//创建接口的匿名实现类的匿名对象
		com.transferData(new USB() {

			@Override
			public void start() {
				System.out.println("MP3开始工作");
			}
			@Override
			public void stop() {
				System.out.println("MP3停止工作");
			}
		});
		}
}
```

总结：对于抽象类与接口，声明(非)匿名类(非)匿名对象的方式基本相同。以匿名类的非匿名对象为例，还是在强制实例化一个抽象类或接口，只不过是在创建的时候通过代码块重写了抽象类或接口中的所有抽象方法。



## 父类与接口中有同名属性时，子类调用方法

```Java
interface A{
	int x=1;
	int y1=3;
}
class B{
	int x=2;
	int y2=4;
}
class C extends B implements A{
	public void show() {
		System.out.println(x);//编译报错
		System.out.println(super.x);//1
		System.out.println(A.x);//2
		System.out.println(y1);//3
		System.out.println(y2);//4
	}
}
public class ExtendsOfInterface {

	public static void main(String[] args) {
		C test=new C();
		test.show();
	}
}
```

Java8以后实现类调用接口中静态与非静态方法的方式

```java
class  SubClass implements CompareA{
	public void myMethod() {
        //默认方法必须被重写，静态方法可不被重写
        //以下两种调用必须发生在实现类的某个函数体内
		CompareA.method1();//调用接口中静态方法
		CompareA.super.method2();//调用接口中非静态方法(规定格式)
	}
}
```



| 结构相同 | 父类                                                         | 接口                                                         |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 接口与   | 属性：直接调用出错sysout(x)，通过super.x与"接口名.x"分别调用；                                                                                             方法：若方法还没有被重写(JDK8以后)，默认调用父类方法。若已经被重写(或必须被重写JDK7及以前)，调用重写后的方法 | 属性：直接调用出错sysout(x)，通过"接口名.x"的方式分别调用；                                                                                          方法：实现类通过一个方法就会重写两个接口中的相同方法，此时调用的时重写后的方法。如果是JDK8以后已经定义好的方法，通过 “接口名.方法” 与“ 接口名.super.方法” 的方式分别调用接口中的静态与非静态方法(但只能在实现类某个函数中调用) |

# ***内部类***

 * 内部类

 * Java中允许将一个类A声明在另一个类B中，则类A就是内部类，类B成为外部类

 * 内部类的分类：成员内部类(静态的、非静态的)、局部内部类(方法内、代码块内、构造器内)

 * 成员内部类：
			一方面，作为外部类的成员：
					可以调用外部类的结构
					可以被static修饰(static不能修饰外部类)
					可以被四种不同权限修饰
	
	另一方面，作为一个类：
	
	​				类内可以定义属性、方法、构造器	
	
	​				可以被final修饰，表示此类不能被继承，言外之意，此类可以被继承
	
	​				可以被abstract修饰
	
	​				如何实例化成员内部类的对象
	
	​				如何在成员内部类中区分调用外部类的结构
	
	```java
	public class InnerClassTest {
	
		public static void main(String[] args) {
			
			//创建Dog实例(静态的成员内部类)
			Person.Dog dog=new Person.Dog();
			dog.show();
			
			//创建Bird实例(非静态的内部成员类)
	//		Person.Bird bird=new Person.Bird();	//编译报错
			Person p=new Person();
			Person.Bird bird=p.new Bird();
			bird.sing();
			bird.display("hahaha");
		}
	}
	class Person{
	
		String name="Simon";
		int age;
		public void eat() {
			System.out.println("human eat");
		}
		class Bird{
			String name="Kitty";
			public Bird() {
				
			}
			public void sing() {
				System.out.println("I am a bird");
				Person.this.eat();//调用外部类的属性，Person.this.可以省略
			}
			public void display(String name) {
				System.out.println(name);//调用形参
				System.out.println(this.name);//调用内部类的属性
				System.out.println(Person.this.name);//调用外部类的属性
			}
		}
		static class Dog{
			String name;
			int age;
			public void show() {
				System.out.println("Kala is a dog");
			}
		}
	}
	```
	
	

# ***异常*** (Error与Exception)

## 1.异常处理：抓抛模(try-catch-finally)

 * 抛：在程序正常执行的过程中，一旦出现了异常，就会在异常代码处生成一个对应异常类的对象，并将此对象抛出

   ​		一旦抛出对象以后，其后的代码就不再执行

 * 抓：异常的处理方式 try-catch-finally 与 throws

 * try-catch-finally的使用

   try{

   //可能出现异常的代码

   }catch(异常类型1 变量名){

   

   //处理异常方式1

   }catch(异常类型2 变量名){

   

   //处理异常方式2

   }...

   finally{

   //一定会执行的代码 

   }

   

 * 说明：

 * finally是可选的

 * 使用try将可能出现异常代码包装起来，在执行过程中，一旦出现异常，就会生成一个对应异常类的对象，根据此对象

   的类型，去catch中进行匹配

 * 一旦try中的异常对象匹配到某一个catch时，就进入catch中进行异常的处理。一旦处理完成，跳出当前的try-catch

   结构(没有写finally的情况下)。继续执行其后的代码

 * catch中的异常类型，如果没有子父类关系，则书写顺序无关。

 * catch中的异常类型，如果满足子父类关系，则子类在前，父类在后。否则报错

 * 常用的异常对象处理方式：String e.getMessage()  与  e.printStackTrace()

 * 在try结构中声明的变量，在出了try结构以后，就不能在被调用

 * try-finally结构可以嵌套

 * finally的使用：finally是可选的

 * finally中声明的是一定会被执行的代码。即使catch中又出现了异常、try中有return语句或

   catch中有return语句等情况，finally中的代码也一定会被执行

 * 总结：使用try-catch-finally处理编译时异常，是让程序在编译时就不再报错，但是运行时仍可能报错

   ​		   相当于我们使用try-catch-finally将一个编译时可能出现的异常，延迟到运行时出现

   ​		   通常情况下，不会针对运行时异常编写try-catch-finally

```java
public class ExceptionTest1 {
	
	@Test
	public void testMethod() {
		int num=method();
		System.out.println(num);//3
	}
	
	public int method() {
		try {
			int[]arr=new int[10];
			//System.out.println(arr[10]);
			return  1;
		}catch(ArrayIndexOutOfBoundsException e) {
			e.printStackTrace();
			return 2;
		}finally {
			System.out.println("我一定会被执行");
			return 3;
		}
	}	
	
	@Test
	public void test1() {
		String str = "123";
		str = "abc";
		try {
			int num = Integer.parseInt(str);
			System.out.println("Hello-----1");
		} catch (NumberFormatException e) {
			//System.out.println("出现数值转换异常");
			//System.out.println(e.getMessage());
			e.printStackTrace();
		}catch(NullPointerException e) {
			System.out.println("空指针异常");
		}
		System.out.println("Hello-----2");
	}
	
	@Test
	public void test2() {
		try {
			int a=10;
			int b=0;
			System.out.println(a/b);
		}catch(ArithmeticException e) {
			//e.printStackTrace();
			int[]arr=new int[10];
			System.out.println(arr[10]);
		}catch(Exception e) {
			e.printStackTrace();
		}finally {
			System.out.println("I am handsome");
		}
		System.out.println("I am handsome");
	}
}
```



## 2.throws +异常类型

 * “throws +异常类型” 写在方法的声明处，指明此方法执行时，可能会抛出的异常类型。一旦当方法体执行时，出现异常，仍会在异常代码处生成一个异常类的对象，此对象若满足throws后异常类型时，就会被抛出。异常代码后续的代码就不再执行了

 * 总结：try-catch-finally：真正的将异常给处理掉了

   ​			throws：只是将异常抛给了方法的调用者，并没有真正将异常处理掉

   ```java
   public class ExceptionTest2 {
   	
   	public static void main(String[] args) {
   		try {
   			method2();
   		}catch(FileNotFoundException e) {
   			e.printStackTrace();
   		}catch(IOException e) {
   			e.printStackTrace();
   		}
   		//method3();
   	
   	}
   	
   	public static void method3() {
   		try {
   			method2();
   		}catch(IOException e) {
   			e.printStackTrace();
   		}
   	}
   	public static void method2() throws FileNotFoundException,IOException{
   		method1();
   	}
   	
   	
   	public static void method1() throws FileNotFoundException,IOException{
   
   		File file = new File("Hello.txt");
   		FileInputStream fis = new FileInputStream(file);
   
   		int data = fis.read();
   		while (data != -1) {
   			System.out.println((char) data);
   			data = fis.read();
   		}
   		fis.close();
   		System.out.println("hhahahahahah");
   	}
   }
   ```

   

   方法重写的规则之一：子类重写的方法抛出的异常类型不大于父类被重写的方法抛出的异常类型

```java
public class OverrideTest {
	public static void main(String[] args) {
		OverrideTest test=new OverrideTest();
		test.display(new SubClass());
	}
	
	public void display(SuperClass s) {
		try {
			s.method();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	
}
class SuperClass{
	public void method() throws IOException{
		
	}
}
class SubClass extends SuperClass{
	public void method() throws FileNotFoundException{
		
	}
}
```

开发中如何选择使用try-catch-finally 还是选择使用throws?

 * 如果父类中被重写的方法没有throws方式处理异常，则子类重写的方法也不能使用throws，意味着如果

   子类重写的方法中有异常，必须使用try-catch-finally方式处理
 * 执行的方法中，先后又调用了另外的几个方法，这几个方法是递进关系执行的，建议这几个方法使用throws的方式

   进行处理。而执行的方法a可以考虑使用try-catch-finally的方式进行处理

## 3.手动抛出异常(throw关键字)

```java
public class StudentTest {

	public static void main(String[] args) {
		Student s=new Student();
		try {
			s.regist(-1001);
		} catch (Exception e) {
			// TODO Auto-generated catch block
			//e.printStackTrace();
			System.out.println(e.getMessage());
		}
	}
	
}
class Student{
	int id;
	
	public void regist(int id) throws Exception {
		if(id>0) {
			this.id=id;
		}else {
			//手动抛出异常对象
			//throw new RuntimeException("输入数据非法");
			
			//定义Exception就要考虑编译时异常
			throw new Exception("输入数据非法");//此时需要对此异常进行处理，选择throws方式处理
		}
	}
}
```

## 4.自定义异常类

步骤：

 * 继承于RuntimeException、Exception

 * 提供全局常量(static final):serialVersionUID

 * 提供重载构造器

   ```java
   public class MyException extends RuntimeException{
   	
   	static final long serialVersionUID = -7034897190745766939L;
   	
   	public MyException() {
   		
   	}
   	
   	public MyException(String msg) {
   		super(msg);
   	}
   }
   ```

   ## 5.异常综合练习

```java
public class ExceptionExercise {
	
	public static void main(String[] args) {
		
		try {
			int i=Integer.parseInt(args[0]);
			int j=Integer.parseInt(args[1]);
			
			int  result=ecm(i,j);
		}catch (NumberFormatException e) {
			System.out.println("数据类型不一致");
		}catch(ArrayIndexOutOfBoundsException e) {
			System.out.println("缺少命令行参数");
		}catch(ArithmeticException e) {
			System.out.println("除0");
		}catch (EcDef e) {
			System.out.println(e.getMessage());
		}	
	}
	
	public static int ecm(int i,int j) throws EcDef {
		if(i<0||j<0) {
			throw new EcDef("分子或分母为负数了!");
		}
		return i/j;
	}

}

//自定义异常类
class EcDef extends Exception{
	
	static final long serialVersionUID=-33875164229948L;
	
	public EcDef() {
		
	}
	
	public EcDef(String msg) {
		super(msg);
	}
	
}
```

# ***多线程***

## 1.方式一：创建Thread类的子类

1.创建一个Thread类的子类  
2.重写Thread类的run()方法，将此线程执行的操作声明在run()方法中
3.创建Thread类的子类的对象
4.通过此对象调用start()方法

注意： 不能让已经start的线程再次start，会抛出IllegalThreadState异常，需要在创建一个新对象再次执行线程

​			不能通过“对象.run()”的方式启动线程，而应该通过“对象.start()”

```java
class MyThread extends Thread{
    @Override
    public void run() {
        for (int i=0;i<100;i++){
            if(i%2==0){
                System.out.println(Thread.currentThread().getName()+":"+i);
            }
        }

    }
}
public class ThreadTest {

    public static void main(String[] args) {

        MyThread t1= new MyThread();
        t1.start();
        //t1.run(); 若调用run()方法，则不会创建出新线程，即均在主线程中执行
        //不能让已经start的线程再次start，会抛出IllegalThreadState异常，需要在创建一个新对象再次执行线程

        //以下操作仍然是在main线程中执行
        for (int i=0;i<100;i++){
            if(i%2==0){
                System.out.println(Thread.currentThread().getName()+":"+i);
            }
        }
    }
}

```

```java
package Thread;
/**
 * 创建两个分线程，一个遍历100以内偶数，另一个遍历100以内奇数
 * @author lycprimer
 * @create 2021-01-04 15:08
 */
public class ThreadExercise {

    public static void main(String[] args) {

//        MyThread1 m1=new MyThread1();
//        MyThread2 m2=new MyThread2();
//
//        m1.start();
//        m2.start();
        //创建Thread类的匿名子类的方式
        new Thread(){
            @Override
            public void run() {
                for(int i=0;i<100;i++){
                    if(i%2==0)
                        System.out.println(Thread.currentThread().getName()+":"+i);
                }
            }
        }.start();

        new Thread(){
            @Override
            public void run() {
                for(int i=0;i<100;i++){
                    if(i%2!=0)
                        System.out.println(Thread.currentThread().getName()+":"+i);
                }
            }
        }.start();

    }
}

class MyThread1 extends  Thread{
    @Override
    public void run() {
        for(int i=0;i<100;i++){
            if(i%2==0)
            System.out.println(Thread.currentThread().getName()+":"+i);
        }
    }
}

class MyThread2 extends  Thread{
    @Override
    public void run() {
        for(int i=0;i<100;i++){
            if(i%2!=0)
            System.out.println(Thread.currentThread().getName()+":"+i);
        }
    }
}


```

## 2.Thread类中常用方法

1.start()方法：启动当前线程，调用当前线程的run()方法
2.run()方法：通常此方法要被重写，将创建线程要执行的操作声明在此方法中
3.currentThread()方法：静态方法，返回执行当前代码的线程
4.getName()方法：获取当前线程的名字
5.setName()方法：设置当前线程的名字
6.yield()方法：释放当前CPU的执行权(但仍可能在下一时刻被分配回来)
7.join()方法：在线程a中调用线程b的join()方法，此时线程a进入阻塞状态直到线程b完全执行完后，线程a才结束阻塞状态
8.sleep(long millitime)方法：让当前线程睡眠指定的millitime毫秒，在指定的millitime毫秒时间内，当前线程是阻塞状态，											  如果在另一线程中此线程对象调用了join()方法，那么那个线程也要随之阻塞
9.isAlive()方法：判断当前线程是否存活，返回值为boolean类型

10.设置当前线程的优先级：
getPriority()方法：获取线程优先级
setPriority(int p)方法：设置线程优先级
说明：高优先级的线程要抢占低优先级线程CPU的执行权。但是只是从概率上讲，高优先级的线程高概率的情况下被执行，并不意味着只有当高优先级的线程执行完以后，低优先级的线程才执行 

```java
class HelloThread extends  Thread{
    @Override
    public void run() {
        for(int i=0;i<100;i++){
            if(i%2==0){
                try {
                    this.sleep(10);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
                System.out.println(Thread.currentThread().getName()+":"+i);
            }
            if(i%20==0){
                this.yield();//释放当前CPU执行权
            }
        }
    }

    public HelloThread(String name){
        super(name);
    }
}
public class ThreadMethod {

    public static void main(String[] args) {
        
        //给分线程命名(两种方式)
        HelloThread h1=new HelloThread("线程1");
        //h1.setName("线程1");
         //给主线程命名
        Thread.currentThread().setName("主线程");
        
        h1.start();
        
        for(int i=0;i<100;i++){
            if(i%2==0){
                System.out.println(Thread.currentThread().getName()+":"+i);
            }
            if(i==20){
                try {
                    h1.join();
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
        System.out.println(h1.isAlive());
    }
}
```

## 3.方式二：实现Runnable接口

1.创建一个实现了Runnable接口的类
2.实现类去实现Runnable中的抽象方法：run()
3.创建实现类的对象
4.将此对象作为参数传递到Thread类的构造器中，创建Thread类的对象
5.通过Thread类的对象调用start()

```java
class MThread implements Runnable{

    @Override
    public void run() {
        for(int i=0;i<100;i++){
            if(i%2==0){
                System.out.println(Thread.currentThread().getName()+":"+i);
            }
        }
    }
}

public class ThreadTest2 {

    public static void main(String[] args) {

        MThread mThread=new MThread();
        //Thread构造器中有一个构造器的参数为Runnable接口，所以可以用Runnable接口的实现类作为形参(接口的多态性)
        Thread thread1=new Thread(mThread);

        thread1.setName("线程1");
        //Thread类中声明了一个Runnable类型的属性。该属性为null时，调用Thread类中的run()方法
        //该属性不为null时，调用的是该属性中的run()方法。
        //而调用Thread的构造器已经为该属性初始化
        /*底层源码如下:
            private Runnable target;
            @Override
            public void run() {
                 if (target != null) {
                  target.run();
                 }
            }
         */
        thread1.start();

        //在启动一个线程，遍历100以内的偶数
        Thread thread2=new Thread(mThread);
        thread2.setName("线程2");
        thread2.start();
    }
}

```

## 4.两种创建线程方式的比较

创建Thread类的子类：声明Thread的子类，并重写Thread类中的run()方法，使得每次创建该子类后，子类调用的是重写									后的方法。但是无法使多个线程共享数据，除非另外声明static。

实现Runnable接口：声明Runnable的实现类，并重写了Runnable接口中的run()方法，且在创建Thread类对象时，调用的								 是有参(参数类型为Runnable)构造器，为Thread类中的Runnable属性初始化，使得在执行Thread类								 中run()方法时，实际执行的是Thread类中Runnable类型属性中的run()方法，且该方法已经被开头声								 明的实现类重写。这种创建方式天然使得多个线程能够共享数据

总结：两种方式都是在重写run()方法，且都是在重写Runnable接口中的run()方法，因为Thread类本身也是Runnable接口		   的实现类。只不过第一种方式是在重写Thread类从Runnable接口“继承”来的run()方法，第二种方式是在重写  		                     		  Thread类中声明为Runnable类型的属性中的run()方法。

## 5.线程的生命周期

![](Java笔记.assets/Threadlife-1609759343012.png)

## 6.线程安全

问题：卖票过程中，出现了重票和错票

原因：当某个线程操作车票的过程中，尚未操作完成时，其他线程参与进来，也操作车票

解决：当一个线程在操作车票的时候，其他线程不能参与进来，直到线程a操作完车票后，其他线程参可以操作车票
     即使线程a出现了阻塞，也不能被改变



 在Java中，通过同步机制，来解决线程的安全问题

###  1.方式一：同步代码块

 synchronized(同步监视器){

 //需要被同步的代码(操作共享数据的代码)

  }
  说明：同步监视器，俗称 “锁”。任何一个类的对象都可以充当锁。要求：多个线程必须要共用同一把锁

​			 在实现类创建多线程的方式中，可以考虑使用this充当同步监视器。

#### (1).实现类线程通过同步代码块实现线程安全

```java
class Window1 implements Runnable{
    private int ticket=100;
    Object obj=new Object();

    @Override
    public void run() {
        while (true){
            synchronized(obj) {
                if (ticket > 0) {
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }

                    System.out.println(Thread.currentThread().getName() + "买票，票号为：" + ticket);
                    ticket--;
                } else {
                    break;
                }
            }
        }
    }
}

public class TicketWindow2 {
    public static void main(String[] args) {

        Window1 w=new Window1();

        Thread t1=new Thread(w);
        Thread t2=new Thread(w);
        Thread t3=new Thread(w);

        t1.setName("窗口1");
        t2.setName("窗口2");
        t3.setName("窗口3");


        t1.start();
        t2.start();
        t3.start();

    }
}
```

#### (2).继承类线程通过同步代码块实现线程安全

与实现类不同的是，继承类天生无法使多个线程共享数据。所以继承类的属性都要声明为static

在继承类创建多线程的方式中，慎用this充当同步监视器，可以使用当前类充当同步监视器

```java
class Window extends Thread{
    private static int ticket=100;
    private static Object obj=new Object();
    @Override
    public void run() {

        while (true){
            synchronized(obj) {
                if (ticket > 0) {

                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }

                    System.out.println(this.getName() + "卖票，票号为：" + ticket);
                    ticket--;
                } else {
                    break;
                }
            }
        }
    }
}

public class TicketWindow {

    public static void main(String[] args) {

     Window w1=new Window();
     Window w2=new Window();
     Window w3=new Window();

     w1.setName("窗口1");
     w2.setName("窗口2");
     w3.setName("窗口3");

     w1.start();
     w2.start();
     w3.start();
    }
}
```

### 2.方式二：同步方法

#### (1).实现类线程通过同步方法实现线程安全

```java
class Window3 implements Runnable{
    private int ticket=100;

    @Override
    public void run() {
        while (true){
            show();
        }
    }

    private synchronized void show(){//同步监视器为this
        if (ticket > 0) {
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            System.out.println(Thread.currentThread().getName() + "买票，票号为：" + ticket);
            ticket--;
        }else{
            Thread.currentThread().stop();
        }
    }
}


public class TicketWindow3 {
    public static void main(String[] args) {

        Window3 w=new Window3();

        Thread t1=new Thread(w);
        Thread t2=new Thread(w);
        Thread t3=new Thread(w);

        t1.setName("窗口1");
        t2.setName("窗口2");
        t3.setName("窗口3");


        t1.start();
        t2.start();
        t3.start();

    }
}

```

#### (2).继承类线程通过同步代码块实现线程安全

```java
class Window4 extends Thread{
    private static int ticket=100;

    @Override
    public void run() {

        while (true){
           show();
        }
    }
    private static synchronized void show(){//无static时同步监视器为this(w1,w2,w3),无法实现线程安全，                                               //有static时同步监视器为Window4.class,可以实现线程安全
        								 //总之，要保证同步监视器唯一
        if (ticket > 0) {
            try {
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

            System.out.println(Thread.currentThread().getName() + "卖票，票号为：" + ticket);
            ticket--;
        }else{
            Thread.currentThread().stop();
        }
    }

}

public class TicketWindow4 {

    public static void main(String[] args) {

        Window4 w1=new Window4();
        Window4 w2=new Window4();
        Window4 w3=new Window4();

        w1.setName("窗口1");
        w2.setName("窗口2");
        w3.setName("窗口3");

        w1.start();
        w2.start();
        w3.start();

    }
}
```

### 3.方式三：Lock锁---->JDK5.0新增

```java
class Windows implements Runnable{
    private int ticket=100;

    //1.实例化ReentrantLock
    private ReentrantLock  lock=new ReentrantLock(true);    //快捷键：ctrl + P  查看构造器形参列表

    @Override
    public void run() {
        while(true){
            try{//调用try-finally也许是因为想借助finally的必执行性，使之执行unlock()
                //2.调用锁定方法:lock()
                lock.lock();
                if(ticket>0){
                    try {
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println(Thread.currentThread().getName()+"卖票，票号为："+ticket);
                    ticket--;
                }else{
                    break;
                }

            }finally {
                //3.调用解锁方法:unlock()
                lock.unlock();
            }
        }
    }
}
public class LockTest {

    public static void main(String[] args) {
        Windows w=new Windows();

        Thread t1=new Thread(w);
        Thread t2=new Thread(w);
        Thread t3=new Thread(w);

        t1.setName("窗口1");
        t2.setName("窗口2");
        t3.setName("窗口3");

        t1.start();
        t2.start();
        t3.start();
    }
}
```

## 7.线程通信

线程通信例子：使用两个线程打印1~100，交替打印

涉及到的三个方法
	wait()：一旦执行此方法，当前线程就进入阻塞状态，并释放同步监视器
	notify()：一旦执行此方法，就会唤醒被wait的一个线程，如果有多个线程wait，则唤醒优先级最高的线程
	notifyAll():一旦执行此方法，就会唤醒所有被wait的线程



说明：1.wait()、notify()、notifyAll()三个方法必须使用在同步代码块或同步方法中
     	  2.wait()、notify()、notifyAll()三个方法的调用者必须是同步代码块或同步代码块中的同步监视器，否则会出现
		      IllegalMonitorStateException异常
           3.wait()、notify()、notifyAll()三个方法是定义在java.lang.Object类中



sleep()方法与wait()方法的异同：

相同点：一旦执行方法，就可以使当前的线程进入阻塞状态

不同点：声明位置不同：Thread类中声明sleep()，Object类中声明wait()。

​			  调用要求不同：sleep()可以在任何需要的场景下调用，wait()必须使用在同步代码块或同步方法中

​			  是否释放同步监视器：如果两个方法都使用在同步代码块中，sleep()不会释放同步监视器，wait()会释放同步监												  视器

```java
class Number implements Runnable{

    private int number=1;

    @Override
    public void run() {
        while(true){
            synchronized (this) {  //快捷键 ctrl + alt + t surround(try-catch-finally、synchronized等)
                notify();
                if(number<=100){
                    try {
                        Thread.sleep(10);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println(Thread.currentThread().getName()+":"+number);
                    number++;
                    try {
                       //使得调用如下wait()方法的线程进入阻塞状态,wait()方法会释放同步监视器，区别于sleep()
                        wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }else{
                    break;
                }
            }
        }
    }
}
public class CommunicationTest {
    public static void main(String[] args) {
        Number number=new Number();

        Thread t1=new Thread(number);
        Thread t2=new Thread(number);

        t1.setName("线程1");
        t2.setName("线程2");

        t1.start();
        t2.start();
    }

}
```

生产者、消费者问题：

生产者将产品交给店员，消费者从店员处取走产品
店员一次只能持有固定数量的产品(20个)，如果生产者试图生产更多的产品，店员会叫停生产者
如果店中有空位放产品，店员会通知生产者继续生产
如果店里没有产品了，店员会告诉消费者等待，如果店中有产品了在通知消费者来取走产品

```java
class Clerk{

    private int productCount=0;
    //生产产品
    public synchronized void produceProduct() {
        if(productCount<20){
            productCount++;
            System.out.println(Thread.currentThread().getName()+"：开始生产第"+productCount+"个产品");
            notify();
        }else{
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
    //消费产品
    public synchronized void consumeProduct() {
        if(productCount>0){
            System.out.println(Thread.currentThread().getName()+"：开始消费第"+productCount+"个产品");
            productCount--;
            notify();
        }else{
            try {
                wait();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}

class Producer extends Thread {

    private Clerk clerk;

    public Producer(Clerk clerk){
        this.clerk=clerk;
    }

    @Override
    public void run() {
        System.out.println(getName()+"：开始生产产品......");
        while(true){
            try {
                Thread.sleep(10);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            clerk.produceProduct();
        }
    }
}

class Consumer extends  Thread{

    private Clerk clerk;

    public Consumer (Clerk clerk){
        this.clerk=clerk;
    }

    @Override
    public void run() {
        System.out.println(getName()+"：开始消费产品......");
        while(true){
            try {
                Thread.sleep(20);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            clerk.consumeProduct();
        }
    }
}

public class ProductTest {

    public static void main(String[] args) {
        Clerk clerk=new Clerk();

        Producer p1=new Producer(clerk);
        p1.setName("生产者1");

        Consumer c1=new Consumer(clerk);
        c1.setName("消费者1");

        Consumer c2=new Consumer(clerk);
        c2.setName("消费者2");

        p1.start();
        c1.start();
        c2.start();
    }
}
```

## 8.创建线程的方式三：实现Callable接口

1.创建一个实现Callabel的实现类 
2.实现call()方法，将此线程需要执行的操作声明在call()中
3.创建Callable接口实现类的对象
4.将此Callable接口实现类的对象作为参数传递到FutureTask构造器中，创建FutureTack类的对象
5.将FutureTask的对象作为参数传递到Thread类的构造器中，创建Thread对象，并start()
6.获取Callable中的call()方法的返回值,get()方法的返回值即为FutureTask构造器参数Callable实现类重写的call()的返回值

```java
class NumThread implements Callable{

    //2.实现call()方法，将此线程需要执行的操作声明在call()中
    @Override
    public Object call() throws Exception {
        int sum=0;
        for(int i=1;i<=100;i++){
            if(i%2==0){
                System.out.println(i);
                sum+=i;
            }
        }
        return sum;
    }
}
public class ThreadNew {

    public static void main(String[] args) {
        //3.创建Callable接口实现类的对象
        NumThread numThread=new NumThread();
        //4.将此Callable接口实现类的对象作为参数传递到FutureTask构造器中，创建FutureTack类的对象
        FutureTask futureTask = new FutureTask(numThread);
        //5.将FutureTask的对象作为参数传递到Thread类的构造器中，创建Thread对象，并start()
        new Thread(futureTask).start();

        try {
            //6.获取Callable中的call()方法的返回值
            //get()方法的返回值即为FutureTask构造器参数Callable实现类重写的call()的返回值
            Object sum = futureTask.get();
            System.out.println("总和为："+sum);
        } catch (InterruptedException e) {
            e.printStackTrace();
        } catch (ExecutionException e) {
            e.printStackTrace();
        }
    }

}
```

## 9.方式四：使用线程池

1.提供指定线程数量的线程池
2.执行指定的线程的操作。需要提供实现Runnable接口或Callable接口的实现类的对象
3.关闭连接池

```java
class NumberThread implements Runnable{
    @Override
    public void run() {
        for(int i=0;i<=100;i++){
            if(i%2==0){
                System.out.println(Thread.currentThread().getName()+":"+i);
            }
        }
    }
}

class NumberThread2 implements Runnable{
    @Override
    public void run() {
        for(int i=0;i<=100;i++){
            if(i%2!=0){
                System.out.println(Thread.currentThread().getName()+":"+i);
            }
        }
    }
}

public class ThreadPool {

    public static void main(String[] args) {
        //1.提供指定线程数量的线程池
        ExecutorService service= Executors.newFixedThreadPool(10);
        //2.执行指定的线程的操作。需要提供实现Runnable接口或Callable接口的实现类的对象
        service.execute(new NumberThread());//适合使用于Runnable
        service.execute(new NumberThread2());
       //service.submit();//适合使用于Callable

        //3.关闭连接池
        service.shutdown();
    }
}
```





# ***常用类***

## 1.字符串相关类

### (1).String类

String的实例化方式：
	  方式一：字面量定义
 	 方式二：new + 构造器

String s=new String("abc")创建了两个对象。一个是堆空间中new结构，另一个是char[]对应的常量池中的数据："abc"

1.String类被声明为final，不能被继承
2.String实现了Serializable接口：表示字符串支持序列化
        实现了Comparable接口：可以比较大小
3.String内部定义了final char[]value用于存储字符串数据
4.String代表不可变的字符序列，即不可变性
    体现：1.当对字符串重新赋值时，需要重写指定内存区域赋值，不能使用原有的value进行赋值
         	  2.当对现有的字符串进行连接操作时，也需要重写指定内存区域赋值，不能使用原有的value进行赋值
        	   3.当调用String类的replace()方法修改字符或字符串时，也需要重写指定内存区域赋值，不能使用原有的value进				  行赋值
5.通过字面量的方式(区别于new)给一个字符串赋值，此时的字符串值声明在字符串常量池中。
6.字符串常量池中是不会存储相同内容的字符串的

![](Java笔记.assets/String.png)

```java
 	    String s1="JavaEE";
        String s2="JavaEE";
        //通过new + 构造器的方式定义，此时s3和s4保存地址值，
        String s3=new String("JavaEE");
        String s4=new String("JavaEE");
	   System.out.println(s1==s2);//true
        System.out.println(s1==s3);//false
        System.out.println(s1==s4);//false
        System.out.println(s3==s4);//false

	   Person p1=new Person("Tom");
        Person p2=new Person("Tom");
        System.out.println(p1.name==p2.name);//true

        Person p3=new Person(new String("Tom"));
        Person p4=new Person("Tom");
        System.out.println(p3.name==p4.name);//false
```

```java
 @Test
    public void test3(){
        String s1="javaEE";			//javaEE
        String s2="hadoop";			//hadoop

        String s3="javaEEhadoop";	//javaEEhadoop
        String s4="javaEE"+"hadoop";	//javaEEhadoop
        String s5=s1+"hadoop";		//javaEEhadoop
        String s6="javaEE"+s2;		//javaEEhadoop
        String s7=s1+s2;			//javaEEhadoop

        System.out.println(s3==s4);//true，均位于字符串常量池中
        System.out.println(s3==s5);//false，s3位于常量池中，s5位于堆中
        System.out.println(s3==s6);//false，s3位于常量池中，s6位于堆中
        System.out.println(s5==s6);//false，均位于堆空间中，但地址不同
        System.out.println(s3==s7);//false，s3位于常量池中，s7位于堆中
        System.out.println(s5==s7);//false，均位于堆空间中，但地址不同
        System.out.println(s6==s7);//false，均位于堆空间中，但地址不同

        String s8=s5.intern();//返回值得到的s8使用的常量值中已经存在的"javaEEhadoop"
        System.out.println(s8==s3);//true

        /*
            结论：常量与常量的拼接结果在常量池中
                 只要其中有一个是变量，拼接结果就在堆中
                 如果拼接的结果调用intern()方法，返回值在常量池中
         */

    }
```

```java
  String str=new String("good");
    char[]ch={'t','e','s','t'};

    public void change(String s,char ch[]){
        s="test ok";
        ch[0]='b';
    }
    public static void main(String[] args) {
        StringClass ex=new StringClass();//public StringClass
        ex.change(ex.str,ex.ch);
        System.out.println(ex.str);//good
        System.out.println(ex.ch);//best

    }
```

```java
 	    String s1=new String("hello");
        String s2=s1;//涉及到变量，所以是在堆空间创建
        String s3=s1;//涉及到变量，所以是在堆空间创建

        s2=new String("haha");
        System.out.println(s1==s2);//false
        System.out.println(s1==s3);//true

        //即使是在堆空间中创建的字符串，有多个引用指向该对象，若其中一个引用试图修改字符串，也不能在原地修改
        //而是会分配新的空间储存修改后的字符串，原字符串不变。这就是字符串不可变性体现之一
```



String类常用方法

![](Java笔记.assets/StringMethod.png)

![](Java笔记.assets/StringMethod2.png)

![](Java笔记.assets/StringMethod3.png)

String--->char[]：调用String.toCharArray()

char[]--->String：调用String的构造器

String--->byte[]：调用String.getBytes()

byte[]--->String：调用String的构造器



### (2).StringBuffer与StringBuilder

 String、StringBuffer、StringBuilder三者的异同

 String:不可变的字符序列，底层结构用char[]
 StringBuffer:可变的字符序列，线程安全，效率低，底层结构用char[]
 StringBuilder:可变的字符序列，JDK5.0新增，线程不安全，效率高，底层结构用char[]

  源码分析：
  String str=new String();    //char value[]=new char[0]
  String str1=new String("abc");  //char[] value=new char[]{'a','b','c'};

  StringBuffer sb1=new StringBuffer();    //char[] value=new char[16];创建了一个长度是16的字符数组
  sb1.append('a');    //value[0]='a';
  sb1.append('b');    //value[1]='b';

  StringBuffer sb2=new StringBuffer("abc");   //char[] value=new char["abc".length+16];

  问题一：System.out.println(sb2.length());//3
  问题二：扩容问题，如果要田间的数据底层数组盛不下，那么就需要扩容底层数组
       		  默认情况下，扩容为原来容量的2倍+2，同时将原有数组的元素复制到新的数组

![](Java笔记.assets/StringBufferMethod1.png)

![](Java笔记.assets/StringBufferMethod2.png)

效率：StringBuilder > StringBuffer >>String 

### (3).获取当前时间

1.long time=System.currentTimeMillis();	//返回时间与1970年1月1日0时0分0秒之间以毫秒为单位的时间差

2.java.util.Date类：Date date=new Date();

​								System.out.println(date);

​								date.getTime();	//获取毫秒数

3.SimpleDateFormat格式化与解析日期(是String<---->Date之间的转化，SimpleDateFormate只是格式化工具)

​	Date--->String：格式化。调用SimpleDateFormate对象的formate()方法，格式由创建SimpleDateFormate对象时的构造								器决定

​	String--->Date：解析。调用SimpleDateFormate对象的parse()方法，会抛出异常，String格式应与SimpleDateFormate								构造器匹配

```java
 @Test
    public void test1() throws ParseException {//此处抛出异常

        //实例化SimpleDateFormat：使用默认构造器
        SimpleDateFormat sdf=new SimpleDateFormat();

        //格式化：日期--->字符串
        Date date=new Date();
        System.out.println(date);

        String format = sdf.format(date);
        System.out.println(format);

        //解析：字符串--->日期
        String str="21-01-07 上午10:59";
        Date date1 = sdf.parse(str);

        System.out.println(date1);

        System.out.println("**********************");
        //********************按照指定方式格式化*******************
        //使用指定带参构造器
        //格式化
        //SimpleDateFormat sdf1 = new SimpleDateFormat("yyyyy.MMMMM.dd GGG hh:mm aaa");
        SimpleDateFormat sdf1 = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
        String format1 = sdf1.format(date);
        System.out.println(format1);
        //解析
        Date parse = sdf1.parse("2021-01-07 11:06:55");
        System.out.println(parse);

    }
```

4.Calendar类

```java
@Test
    public void test2(){
        //Calendar类(抽象类)的使用

        //方式一：创建其子类(GregorianCalendar)对象
        //方式二：调用其静态方法getInstance()

        Calendar c = Calendar.getInstance();//返回值是Calendar,但对象是由其子类创建的
        System.out.println(c.getClass()); //class java.util.GregorianCalendar

        //常用方法

        //get()
        int days = c.get(Calendar.DAY_OF_MONTH);//今天是今月的第几天
        System.out.println(days);
        System.out.println(c.get(Calendar.DAY_OF_YEAR));//今天是今年的第几天

        //set()
        c.set(Calendar.DAY_OF_MONTH,22);
        int day2 = c.get(Calendar.DAY_OF_MONTH);
        System.out.println(day2);

        //add()
        c.add(Calendar.DAY_OF_MONTH,3);
        int day3 = c.get(Calendar.DAY_OF_MONTH);
        System.out.println(day3);

        //getTime()：日历类--->Date
        Date date = c.getTime();
        System.out.println(date);

        //setTime()：Date--->日历类
        Date date1=new Date();
        c.setTime(date1);
        System.out.println(c.get(Calendar.DAY_OF_MONTH));

    }
```

### 2.自定义类对象间的比较

#### (1).实现Comparable接口(自然排序)

String类、包装类等实现了Comparable接口，重写了compareTo()方法，调用后进行从大到小排列

 重写compareTo(obj)规则：
  如果当前对象this大于形参obj，则返回正整数
  如果当前对象this小于形参obj，则返回负整数
  如果当前对象this等于形参obj，则返回零

  对于自定义类如果需要排序，需要让自定义类实现Comparable接口，重写comparable(obj)方法，在comparable(obj)方法中指明如何排序

```java
class Goods implements Comparable{
    private String name;
    private double price;

    public Goods(String name, double price) {
        this.name = name;
        this.price = price;
    }


    @Override
    public String toString() {
        return "Goods{" +
                "name='" + name + '\'' +
                ", price=" + price +
                '}';
    }

    @Override
    public int compareTo(Object o) {
        if(this==o){
            return 0;
        }

        if(o instanceof Goods){
            Goods goods=(Goods) o;
            if(this.price>goods.price){
                return 1;
            }else if(this.price< goods.price){
                return -1;
            }else{
                //价格相同的情况下，按照名字排序
                return this.name.compareTo(goods.name);
            }
        }
        else{
            throw new RuntimeException("传入的数据类型不一致");
        }
    }
}
public class ComparableTest {

    public static void main(String[] args) {
        Goods[]arr=new Goods[6];
        arr[0]=new Goods("联想Mouse",34);
        arr[1]=new Goods("戴尔Mouse",43);
        arr[2]=new Goods("小米Mouse",12);
        arr[3]=new Goods("MinusMouse",65);
        arr[4]=new Goods("DajiangMouse",65);
        arr[5]=new Goods("MicrosoftMouse",65);

        Arrays.sort(arr);
        System.out.println(Arrays.toString(arr));

    }

}
```

#### (2).实现Comparator接口(定制排序)

```java
定制排序会覆盖自然排序的排序方法，即toCompare()方法
@Test
    public void test1(){

        String[]arr=new String[]{"AA","CC","KK","MM","GG","JJ","DD"};
        Arrays.sort(arr,new Comparator(){

            //按照字符串从大到小的顺序排列
            @Override
            public int compare(Object o1, Object o2) {
                if(o1 instanceof String&& o2 instanceof String){
                    String s1=(String) o1;
                    String s2=(String)o2;
                    return -s1.compareTo(s2);
                }else{
                    throw new RuntimeException("输入的数据类型不一致");
                }


            }
        });

        System.out.println(Arrays.toString(arr));

    }
```

```java
 @Test
    public void test2(){

        Goods[]arr=new Goods[6];
        arr[0]=new Goods("LenovoMouse",34);
        arr[1]=new Goods("DellMouse",43);
        arr[2]=new Goods("XiaomiMouse",12);
        arr[3]=new Goods("MinusMouse",65);
        arr[4]=new Goods("DajangMouse",65);
        arr[5]=new Goods("MicrosoftMouse",65);

        Arrays.sort(arr,new Comparator(){
            //先按名称从低到高，再按价格从高到低排序
            @Override
            public int compare(Object o1, Object o2) {
                if(o1 instanceof Goods&& o2 instanceof Goods){
                    Goods g1=(Goods) o1;
                    Goods g2=(Goods) o2;
                    if(g1.getName().equals(g2.getName())){

                        return  -Double.compare(g1.getPrice(),g2.getPrice());

                    }else{
                        return g1.getName().compareTo(g2.getName());
                    }
                }else{
                    throw new RuntimeException("数据类型不一致");
                }
            }
        });

        System.out.println(Arrays.toString(arr));
    }
```

Comparable与Comparator对比：Comparable接口的方式一旦指定，保证Comparable接口的实现类的对象在任何位置都													可以比较大小。而Comparator接口属于临时性的比较
                                               



# ***枚举类***

枚举类已经重写过toString()方法，返回的是枚举类中创建的本对象的对象名

枚举类的对象被public static final修饰

枚举类属性被public final修饰

  Enum类中的常用方法:
 values()方法：返回枚举类型的对象数组
 valueOf(String str)方法：把一个字符串转为对应的枚举类对象
 toString():返回当前枚举类对象常量的名称(在没有重写的前提下)

 使用enum关键字定义的枚举类实现接口的情况:
 情况一：实现接口，在enum类中实现抽象方法
 情况二：枚举类的不同对象分别实现接口中的抽象方法

理解：枚举类中存在对象、属性、方法。属性与方法不仅仅服务于类，还服务于对象，也就是说，在枚举类中有本枚举类    			的对象。

```java
public class EnumClassTest2 {
    public static void main(String[] args) {
        Season2 summer = Season2.SUMMER;
        System.out.println(summer);
        System.out.println(Season2.class.getSuperclass());//class java.lang.Enum
        System.out.println("********************************************");

        //values()方法
        Season2[] values = Season2.values();
        for(int i=0;i<values.length;i++){
            System.out.println(values[i]);
            values[i].show();
        }

        System.out.println("**********************************************");
        Thread.State[] states = Thread.State.values();
        for(int i=0;i<states.length;i++){
            System.out.println(states[i]);
        }
        System.out.println("**********************************************");
        //valueOf(String objName)方法:返回枚举类中对象名是objName的对象
        //若没有objName的枚举类对象，则抛异常IllegalArgumentException
        Season2 winter = Season2.valueOf("WINTER");
        System.out.println(winter);

        winter.show();

    }

}
interface Info{
    void show();
}

//自定义枚举类
enum Season2 implements Info{

    //1.提供当前枚举类的对象，多个对象之间用","隔开，末尾对象用";"结束
   SPRING("春天","春暖花开"){
        @Override
        public void show() {
            System.out.println("春天在哪里");
        }
    },
   SUMMER("夏天","夏日炎炎"){
       @Override
       public void show() {
           System.out.println("宁静的夏天");
       }
   },
   AUTUMN("秋天","秋高气爽"){
       @Override
       public void show() {
           System.out.println("秋天不回来");
       }
   },
   WINTER("冬天","冰天雪地"){
       @Override
       public void show() {
           System.out.println("大约在冬季");
       }
   };

    //2.声明Season对象的属性:private final修饰
    private final String seasonName;
    private final String seasonDesc;

    //3.私有化类的构造器，并给对象属性赋值
    private Season2(String seasonName,String seasonDesc){
        this.seasonName=seasonName;
        this.seasonDesc=seasonDesc;
    }


    //4.其他诉求：获取枚举类对象的属性
    public String getSeasonName() {
        return seasonName;
    }

    public String getSeasonDesc() {
        return seasonDesc;
    }

//    @Override
//    public void show() {
//        System.out.println("这是一个季节");
//    }

    //5.其他诉求：提供toString()方法
//    @Override
//    public String toString() {
//        return "Season2{" +
//                "seasonName='" + seasonName + '\'' +
//                ", seasonDesc='" + seasonDesc + '\'' +
//                '}';
//    }
}

```





# ***注解***

 注解(Annotation)的使用：


 自定义注解：注解声明为 @interface
           内部定义成员，通常使用value表示，其属性是以方法的形式声明的
           可以指定成员的默认值，使用default定义
           如果自定义的注解没有成员，表明是标识作用
           如果注解有成员，在使用注解时，要指定成员的值，指定了默认值的除外
           自定义注解必须配合上注解的信息处理流程(反射)才有意义
           自定义注解通常会指明两个元注解：Retention、Target


 JDK中提供的4种元注解：Retention、Target、Documented、Inherited
 元注解：对现有的注解进行解释说明的注解(修饰注解的注解)
  Retention:指定所修饰的Annotation的生命周期：SOURCE\CLASS(默认行为)\RUNTIME
            只有声明为RUNTIME生命周期的注解，才能通过反射获取
  Target:用于指定被修饰的Annotation能用于修饰那些程序元素
  Documented:用于指定被该元注解修饰Annotation类在被javadoc解析时，保留下来
  Inherited:被该元注解修饰的Annotation将具有继承性，如果某个类使用类别@Inherited修饰的Annotation，则其
            子类将自动具有该注解

  JDK8中注解的新特性：可重复注解、类型注解



# ***Java集合***

 集合、数组都是对多个数据进行存储操作的结构，简称Java容器。

 集合架构
  |----Collection接口：单列集合，用来存储单个对象
          |----List接口：存储有序、可重复的数据。---->动态数组
             	 |----ArrayList、LinkedList、Vector

​		  |----Set接口： 存储无序、不可重复的数据 ---->集合
​             	 |----HashSet、LinkedHashSet、TreeSet

  |----Map接口：双列集合，用来存储一对数据(key-value 键值对)	---->函数：y=f(x)
        		  |----HashMap、LinkedHashMap、TreeMap、Hashtable、Properties

## 1.Collection接口



### 接口中常用方法

```java
public class CollectionTest {

    @Test
    public void test1(){

        Collection coll=new ArrayList();

        //add():将元素e添加到集合coll中
        coll.add("AA");
        coll.add("BB");
        coll.add("123");
        coll.add(new Date());

        //size()：获取添加元素的个数
        System.out.println(coll.size());

        //addAll(Collection coll):将coll集合中的元素添加到当前的集合中
        Collection coll2=new ArrayList();
        coll2.add(456);
        coll2.add("CC");
        coll2.addAll(coll);
        System.out.println(coll2.size());

        //clear():清空集合元素
        coll.clear();

        //isEmpty():判断当前集合是否为空
        System.out.println(coll.isEmpty());


    }

    @Test
    public void test2(){

        Collection coll=new ArrayList();
        coll.add(123);
        coll.add(456);
        coll.add(new String("Tom"));
        coll.add(false);
        coll.add(456);
        coll.add(new Person("Jerry",20));
        coll.add(new Person("Kitty",21));

        Person p=new Person("Kitty",21);

        //向Collection接口的实现类的对象中添加数据obj时，要求obj所在类要重写equals()方法
        //contains(Object obj):判断当前集合是否包含obj，因此自定义类要重写equals()方法
        //该函数的比较实际是调用obj对象所在类中的equals()方法，通常自定义类要重写equals()方法
        boolean contains = coll.contains(123);
        System.out.println(contains);//true
        System.out.println(coll.contains(new String("Tom")));//true
        System.out.println(coll.contains(p));//false(Person类未重写equals()方法)
                                             //true(Person类重写equals()方法)


        //containsAll(Collection coll2):判断形参coll2中的所有元素是否都存在于当前集合中
        
        Collection coll2= Arrays.asList(123,456);
        System.out.println(coll.containsAll(coll2));//true

    }

    @Test
    public void test3(){
        Collection coll=new ArrayList();
        coll.add(123);
        coll.add(456);
        coll.add(new String("Tom"));
        coll.add(false);
        coll.add(456);
        coll.add(new Person("Jerry",20));
        coll.add(new Person("Kitty",21));

        //remove(Object obj):从当前集合移除obj元素(对于重复元素，最多只会移除一个元素)
        coll.remove(456);
        System.out.println(coll);
        coll.remove(new Person("Jerry",20));
        System.out.println(coll);

        //remove(Collection coll2):从当前集合移除coll2中所有元素
        Collection coll2=Arrays.asList(123,456);
        coll.removeAll(coll2);
        System.out.println(coll);
    }

    @Test
    public void test4(){

        Collection coll=new ArrayList();
        coll.add(123);
        coll.add(456);
        coll.add(new String("Tom"));
        coll.add(false);
        coll.add(456);
        coll.add(new Person("Jerry",20));
        coll.add(new Person("Kitty",21));

        //retainAll(Object coll2):获取当前集合于coll2的交集
        Collection coll2=Arrays.asList(123,456,789);
        coll.retainAll(coll2);
        System.out.println(coll);

        //equals(Object obj):判断当前集合与形参集合是否相同
        Collection coll2=new ArrayList();
        coll2.add(123);
        coll2.add(456);
        coll2.add(new String("Tom"));
        coll2.add(false);
        coll2.add(456);
        coll2.add(new Person("Jerry",20));
        coll2.add(new Person("Kitty",21));

        System.out.println(coll.equals(coll2));//true

    }


    @Test
    public void test5(){

        Collection coll=new ArrayList();
        coll.add(123);
        coll.add(456);
        coll.add(new String("Tom"));
        coll.add(false);
        coll.add(456);
        coll.add(new Person("Jerry",20));
        coll.add(new Person("Kitty",21));

        //hashCode():返回当前对象的哈希值
        System.out.println(coll.hashCode());

        //集合--->数组 toArray()
        Object[] arr = coll.toArray();
        for(int i=0;i<arr.length;i++){
            System.out.println(arr[i]);
        }

        //数组--->集合
        int[]arr=new int[]{1,2,3,4,5};
        List list=new ArrayList();

        for(Integer i:arr){
            list.add(i);
        }
        System.out.println(list);

    }

}
class Person{

    private String name;
    private int age;

    public Person() {

    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        Person person = (Person) o;
        return age == person.age && Objects.equals(name, person.name);
    }


}
```

### 迭代器(iterator)

```java
/**
 *  迭代器(iterator)
 *
 *  注意，迭代器在遍历的过程中，本身也会改变!
 *  集合对象每次调用iterator()方法都会得到一个全新的迭代器对象，默认游标都在集合的第一个元素之前
 *  内部定义了remove()方法，可以在遍历的时候，删除集合中的元素。此方法不同于集合直接调用remove()方法
 */
public class IteratorTest {
    @Test
    public void test1(){
        Collection coll=new ArrayList();
        coll.add(123);
        coll.add(456);
        coll.add(new String("Tom"));
        coll.add(false);
        coll.add(456);
        coll.add(new Person("Jerry",20));
        coll.add(new Person("Kitty",21));

        Iterator iterator = coll.iterator();


        //方式一：
        for(int i=0;i<coll.size();i++){
            System.out.println(iterator.next());
        }
        //方式二：推荐
        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }


    }

    @Test
    public void test2(){
        Collection coll=new ArrayList();
        coll.add(123);
        coll.add(456);
        coll.add(new String("Tom"));
        coll.add(false);
        coll.add(456);
        coll.add(new Person("Jerry",20));
        coll.add(new Person("Kitty",21));

        Iterator iterator = coll.iterator();

        while(iterator.hasNext()){
            Object obj=iterator.next();
            if("Tom".equals(obj)){
                iterator.remove();
            }
        }

        iterator=coll.iterator();
        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }
    }

}
```

### 增强for循环

```java
 @Test
    public void test1(){

        Collection coll=new ArrayList();
        coll.add(123);
        coll.add(456);
        coll.add(new String("Tom"));
        coll.add(false);
        coll.add(456);
        coll.add(new Person("Jerry",20));
        coll.add(new Person("Kitty",21));

        //for(集合元素的类型  局部变量 ：集合对象)
        //内部仍然调用了迭代器
        for(Object obj:coll){
            System.out.println(obj);
        }

    }
    @Test
    public void test2(){

        int[]arr=new int[]{1,2,3,4,5,65};

        //for(数组元素的类型 局部变量：集合对象)
        for(int i:arr){
            System.out.println(i);
        }
    }

    @Test
    public void test3(){
        String []arr=new String[]{"MM","MM","MM"};

        for(int i=0;i<arr.length;i++){
            arr[i]="GG";
        }   //执行结果：字符串数组均改为"GG"

        for(String s:arr){
            s="MM";
        }   //执行结果：字符串数组不变(并不是因为字符串的不可变性，而是arr[i]将值赋给了形参s，只是s更改了)


        for(int i=0;i<arr.length;i++){
            System.out.println(arr[i]);
        }
    }
```

#### List接口中常用方法



```java
/**
 * @author lycprimer
 * @create 2021-01-09 11:00
 *
 *  |----Collection接口：单列集合，用来存储单个对象
 *           |----List接口：存储有序、可重复的数据。---->动态数组
 *              	 |----ArrayList：List接口的主要实现类，线程不安全，效率高。底层使用Object[] 		                                                                                        elementData存储
 *                   |----LinkedList：对于频繁的插入、删除操作，使用此类效率比ArrayList高。线程安全，效率                                                                                      低。底层使用双向链表
 *                   |----Vector:List接口的古老实现类，线程安全，效率低。底层使用Object[]存储
 
 	常用方法：
 	增：add(Object obj)
 	删：remove(int index)/remove(Object obj)
 	改：set(int index,Object obj)
 	查：get(int index)
 	插：add(int index,Object obj)
 	长度：size()
 	遍历：Itetrator、增强for循环、普通for循环
 *
 */
public class LIstInterfaceTest {

    @Test
    public void test1(){

        ArrayList list=new ArrayList();
        list.add(123);
        list.add(456);
        list.add("AA");
        list.add(new String("Tom"));
        list.add(new Person("Jerry",21));
        list.add(456);

        System.out.println(list);

        //void add(int index,Object ele):在index位置插入ele元素
        list.add(1,"BB");
        System.out.println(list);

        //boolean addAll(int index,Collection eles):从index位置开始，将eles中所有元素插入
        List list2= Arrays.asList(1,2,3);
        list.addAll(1,list2);
        System.out.println(list);

        //Object get(int index):获取指定index位置的元素
        System.out.println(list.get(1));

    }

    @Test
    public void test2(){

        ArrayList list=new ArrayList();
        list.add(123);
        list.add(456);
        list.add("AA");
        list.add(new String("Tom"));
        list.add(new Person("Jerry",21));
        list.add(456);

        System.out.println(list);

        //int indexOf(Object obj):返回obj在集合中首次出现的位置,若不存在返回-1
        System.out.println(list.indexOf(456));

        //int lastIndexOf(Object obj):返回obj在集合中最后一次出现的位置,若不存在返回-1
        System.out.println(list.lastIndexOf(456));

        //Object remove(int index):移除指定index位置的元素，并返回此元素
        Object obj = list.remove(0);
        System.out.println(obj);
        System.out.println(list);

        //Object set(int index,Object ele):设置指定index位置的元素为ele
        list.set(1,"CC");
        System.out.println(list);

        //List subList(int fromIndex,int toIndex):返回从fromIndex到toIndex位置的左闭右开区间的子集合
        List subList = list.subList(2, 4);
        System.out.println(list);
        System.out.println(subList);


    }

    @Test
    public void test3(){

        ArrayList list=new ArrayList();
        list.add(123);
        list.add(456);
        list.add("AA");
        list.add(new String("Tom"));
        list.add(new Person("Jerry",21));
        list.add(456);

        //方式一：Iterator迭代器方法
        Iterator iterator = list.iterator();
        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }

        //方式二：增强for循环
        for(Object obj:list){
            System.out.println(obj);
        }

        //方式三：普通for循环
        for(int i=0;i<list.size();i++){
            System.out.println(list.get(i));
        }

    }

}
```

#### Set接口

  |----Collection接口：单列集合，用来存储单个对象
         |----Set接口： 存储无序、不可重复的数据 ---->集合
                   |----HashSet：作为Set接口的主要实现类，线程不安全 
                               |----LinkedHashSet：作为HashSet的子类，遍历其内部数据时会按照添加的顺序遍历
                   |----TreeSet：可以按照添加对象的指定属 性，进行排序

  Set接口中没有额外定义的新方法，使用的都是Collection中声明过的方法

  Set存储无序、不可重复的数据

  无序性：并非随机性。存储的数据在底层数组中并非按照数组索引的顺序添加，而是根据数据的哈希值

  不可重复性：保证添加的元素按照equals()方法判断时，不能返回true。即相同的元素只能添加一个

  添加元素的过程(以HashSet为例)：
      向HashSet中添加元素a，首先调用元素a所在类的hashCode()方法，计算出元素a的哈希值。
      此哈希值影响着着元素a在HashSet底层数组中的存放位置。判断数组此位置上是否已经有了其他元素
      如果此位置上没有其他元素，则元素a添加成功；--->情况1
      如果此位置上有其他元素b(或以链表的形式存在着多个元素)，则比较元素a与元素b的哈希值：
          如果哈希值不相同，则元素a添加成功 --->情况2
          如果哈希值相同，进而调用元素a所在类的equals()方法：
              equals()方法返回ture,元素a添加失败，
              equals()方法返回false,元素a添加成功。--->情况1

比较索引值--->比较哈希值--->调用equals()方法

​	对于添加成功的情况2与情况3而言，元素a与已经存在指定索引位置上的数据以链表的形式存储

  Object类中hashCode()方法算出来的哈希值基本上是随机的，所以自定义类需要重写hashCode()方法

  向Set中添加的数据，其所在类一定要重写hashCode()和equals()
  重写的hashCode()和equals()尽可能保持一致性(相同的对象必须要求相同的哈希值)

```java
public class SetTest {

    @Test
    public void test1(){

        Set set=new HashSet();
        set.add(456);
        set.add(123);
        set.add("AA");
        set.add("CC");
        set.add(new Person("Tom",21));
        set.add(new Person("Tom",21));
        set.add(129);
        set.add(123);

        Iterator iterator = set.iterator();
        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }
    }
}
```

```java
@Test
    public void test2(){

        //LinkedHashSet的使用：LinkedHashSet作为HashSet的子类，在添加数据的同时，每个数据还维护了两个引用。
                    //记录此数据的前一个数据和后一个数据。对于频繁的遍历操作，LinkedHashSet效率高于HashSet
        Set set=new LinkedHashSet();
        set.add(456);
        set.add(123);
        set.add("AA");
        set.add("CC");
        set.add(new Person("Tom",21));
        set.add(new Person("Tom",21));
        set.add(129);
        set.add(123);

        Iterator iterator = set.iterator();
        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }
    }
```

TreeSet

```java
/**
 * @author lycprimer
 * @create 2021-01-09 17:10
 * 向TreeSet中添加的数据，要求是相同类的对象
 * 两种排序方式：自然排序(实现Comparable接口)、定制排序(Comparator)
 *
 * 自然排序中，比较两个对象是否相同的标准是compareTo()返回0，不再是equals()
 * 定制排序中，比较比较两个对象是否相同的标准是compare()返回0，不再是equals()。同时调用有参构造器TreeSet 																	      set=new TreeSet(com)
 	定制排序会覆盖自然排序
 *
 *
 */
public class TreeSetTest {

    @Test
    public void test1(){

        TreeSet set=new TreeSet();
//        不能添加不同类的对象
//        set.add(123);
//        set.add(456);
//        set.add("AA");
//        set.add(new Person("Tom",21));

        set.add(123);
        set.add(122);
        set.add(-21);
        set.add(15);
        set.add(1);

        Iterator iterator = set.iterator();

        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }
    }

    @Test
    public void test2(){

        TreeSet set=new TreeSet();

        set.add(new Persons("Tom",21));
        set.add(new Persons("Jerry",8));
        set.add(new Persons("Kitty",19));
        set.add(new Persons("Jimmy",23));
        set.add(new Persons("Simon",23));
        set.add(new Persons("Simon",23));

        Iterator iterator = set.iterator();

        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }

    }

    @Test
    public void test3(){
        Comparator com=new Comparator() {
            //按照年龄从小到大排序
            @Override
            public int compare(Object o1, Object o2) {
                if(o1 instanceof Persons&&o2 instanceof Persons){
                    Persons p1=(Persons)o1;
                    Persons p2=(Persons)o2;

                    return Integer.compare(p1.getAge(),p2.getAge());
                }else{
                    throw new RuntimeException("输入的数据类型不一致");
                }
            }
        };

        TreeSet set=new TreeSet(com);
        set.add(new Persons("Tom",21));
        set.add(new Persons("Jerry",8));
        set.add(new Persons("Kitty",19));
        set.add(new Persons("Jimmy",23));
        set.add(new Persons("Simon",22));
        set.add(new Persons("Simon",20));

        Iterator iterator = set.iterator();
        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }
    }

}
class Persons implements Comparable{
    private String name;
    private int age;

    public Persons(String name, int age) {
        this.name = name;
        this.age = age;
    }

    //按照姓名从大到小，年龄从小到大
    @Override
    public int compareTo(Object o) {
        if(o instanceof Persons){
            Persons p=(Persons)o;
            int compare=-this.name.compareTo(p.name);
            if(compare!=0){
                return -this.name.compareTo(p.name);
            }else{
                return Integer.compare(this.age,p.age);
            }
        }else{
            throw new RuntimeException("输入的类型不匹配");
        }
    }

    @Override
    public String toString() {
        return "Persons{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
```

## 2.Map接口

![](Java笔记.assets/MapInterface.png)

```java
/**
 * @author lycprimer
 * @create 2021-01-09 19:18
 *
 *  |----Map：双列数据，存储key-value对的数据，类似于y=f(x)
 *          |----HashMap：作为Map的主要实现类。线程不安全，效率高。能存储null的key和value
 *              |----LinkedHashMap：保证在遍历map元素时，可以按照添加的顺序实现遍历
 *                                  原因：在原有的HashMap底层结构的基础上，添加了一对引用，指向前一个与后一个数据
 *                                  对于频繁的遍历操作，该类执行效率高于HashMap
 *          |----TreeMap：保证按照添加的key-value对进行排序，实现排序遍历.(key的自然或定制排序)
 *          |----Hashtable：作为Map的古老实现类。线程安全，效率低。不能存储null的key和value
 *              |----Properties：常用来处理配置文件。其key和value都是String类型
 *
 *       key:无序的、不可重复的---->Set存储
 		value:无序的、可重复的---->Collection存储
  
 *Map结构的理解：
 *    Map中的key：无序的、不可重复的，使用Set存储所有的key  ---->key所在的类要重写 equals()和 hashCode()
 *    Map中的value:无序的、可重复的，使用Collection存储所有的value ---->value所在的类要重写equals()
 *    一个键值对key-value构成一个Entry对象
 *    Map中的entry：无序的、不可重复的，使用Set存储所有的entry
 *
 *HashMap的底层实现原理：
 *  HashMap map=new HashMap()：在实例化后，底层创建了长度是16的一维数组Entry[] table
 
 *  map.put(key,value):
 *  首先，调用key所在类的hashCode()方法计算出key所对应的哈希值，此哈希值影响着在Entry数组中的存放位置。
 *          如果此位置上的数据为空，此时的key-value添加成功。--->情况1
 *          如果此位置上的数据不为空(意味着此位置上存在着一个或多个数据(以链表形式存在))，
 *          比较key与已经存在的一个或多个数据的哈希值：
 *                  如果key的哈希值与已经存在的数据的哈希值都不相同，此时key-value添加成功，--->情况2
 *                  如果key的哈希值和已经存在的某一个数据(key2-value2)的哈希值相同，继续调用key所在类的equals()方法比较：
 *                          如果equals()返回false:此时key-value添加成功，--->情况3
 *                          如果equals()返回true:使用value替换value2
 
 比较索引值--->比较哈希值--->调用equals()方法。与Collection不同的是，若equals()方法返回值为true，进行替换
 *
 * 对于情况2与情况3：此时key-value与原来的数据以链表的方式存储
 *
 * Map中常用方法：
 * 添加：put(Object key,Object value)
 * 删除：remove(Object key)
 * 修改：put(Object key,Object value)
 * 查询：get(Object key)
 * 长度：size()
 * 遍历：keySet()/values()/entrySet()
 *
 */
public class MapTest {

    @Test
    public void test1(){

        Map map=new HashMap();
        //Object put(Object key,Object value)
        map.put("AA",123);
        map.put(45,123);
        map.put("BB",56);

        //修改
        map.put("AA",87);
        System.out.println(map);

        Map map2=new HashMap();
        map2.put("CC",123);
        map2.put("DD",123);

        //putAll(Map m)
        map2.putAll(map);
        System.out.println(map);
        System.out.println(map2);

        //Object remove(Object key)
        Object value = map.remove("AA");
        System.out.println(value);
        System.out.println(map);

        //void clear()
        map.clear();
        System.out.println(map.size());

    }

    @Test
    public void test2(){

        Map map=new HashMap();

        map.put("AA",123);
        map.put(45,123);
        map.put("BB",56);

        //Object get(Object key)
        System.out.println(map.get(45));

        //boolean containsKey(Object key)
        boolean isExist = map.containsKey("BB");
        System.out.println(isExist);

        //boolean containsValue(Object value)
        isExist=map.containsValue(123);
        System.out.println(isExist);

        //boolean isEmpty()
        System.out.println(map.isEmpty());
    }

    @Test
    public void test3(){

        Map map=new HashMap();
        map.put("AA",123);
        map.put(45,123);
        map.put("BB",56);

        //遍历所有的key集 keySet()
        Set set=map.keySet();
        Iterator iterator = set.iterator();
        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }

        //遍历所有的value集 values()
        Collection values=map.values();
        for(Object obj:values){
            System.out.println(obj);
        }

        //遍历所有的key-value

        //方式一：entrySet()
        Set entrySet = map.entrySet();
        Iterator iterator1 = entrySet.iterator();
        while(iterator1.hasNext()){
            Object obj=iterator1.next();
            //entrySet集合中的元素都是Map.entry
            Map.Entry entry=(Map.Entry)obj;
            System.out.println(entry.getKey()+"--->"+entry.getValue());
        }
        //方式二：
        Set keySet=map.keySet();
        Iterator iterator2=keySet.iterator();
        while(iterator2.hasNext()){
            Object key=iterator2.next();
            Object value=map.get(key);
            System.out.println(key+"--->"+value);
        }


        //注意keySet()、values()、entrySet()三者之间的关系

    }

}
```

### TreeMap

```java
public class TreeMapTest {

    //向TreeMap中添加key-value，要求key必须是有同一个类创建的对象
    //因为要按照key进行排序：自然排序、定制排序

    @Test
    public void test1(){

        TreeMap map=new TreeMap();

        Persons p1=new Persons("Tom",21);
        Persons p2=new Persons("Jerry",19);
        Persons p3=new Persons("Kitty",32);
        Persons p4=new Persons("Jimmy",2);

        map.put(p1,97);
        map.put(p2,89);
        map.put(p3,76);
        map.put(p4,100);

        Set entrySet = map.entrySet();
        Iterator iterator = entrySet.iterator();
        while(iterator.hasNext()){
            Object obj=iterator.next();
            Map.Entry entry=(Map.Entry)obj;

            System.out.println(entry.getKey()+"--->"+entry.getValue());
        }
    }

    @Test
    public void test2(){
        
        TreeMap map=new TreeMap(new Comparator() {
            @Override
            public int compare(Object o1, Object o2) {
                if(o1 instanceof Persons&&o2 instanceof Persons){
                    Persons p1=(Persons)o1;
                    Persons p2=(Persons)o2;
                    return Integer.compare(p1.getAge(),p2.getAge());
                }else{
                    throw new RuntimeException("输入的数据类型不一致！");
                }
            }
        });

        Persons p1=new Persons("Tom",21);
        Persons p2=new Persons("Jerry",19);
        Persons p3=new Persons("Kitty",32);
        Persons p4=new Persons("Jimmy",18);

        map.put(p1,97);
        map.put(p2,89);
        map.put(p3,76);
        map.put(p4,100);

        Set entrySet = map.entrySet();
        Iterator iterator = entrySet.iterator();
        while(iterator.hasNext()){
            Object obj=iterator.next();
            Map.Entry entry=(Map.Entry)obj;

            System.out.println(entry.getKey()+"--->"+entry.getValue());
        }

    }


}
class Persons implements Comparable{
    private String name;
    private int age;

    public Persons(String name, int age) {
        this.name = name;
        this.age = age;
    }

    //按照姓名从大到小，年龄从小到大
    @Override
    public int compareTo(Object o) {
        if(o instanceof Persons){
            Persons p=(Persons)o;
            int compare=-this.name.compareTo(p.name);
            if(compare!=0){
                return -this.name.compareTo(p.name);
            }else{
                return Integer.compare(this.age,p.age);
            }
        }else{
            throw new RuntimeException("输入的类型不匹配");
        }
    }

    @Override
    public String toString() {
        return "Persons{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
```

## 3.Collections工具类

```java
/**
 * Collections工具类能操作Collection接口实现类与Map接口实现类
 */
public class CollectionsToolClass {

    @Test
    public void test1(){

        List list=new ArrayList();

        list.add(123);
        list.add(34);
        list.add(21);
        list.add(-23);
        list.add(-11);
        list.add(22);
        list.add(22);
        System.out.println(list);

        //void reverse(List)
        Collections.reverse(list);
        System.out.println(list);

        //void shuffle(List):随机排序
        Collections.shuffle(list);
        System.out.println(list);

        //void sort(List)
        //void sort(List,Comparator)
        Collections.sort(list);
        System.out.println(list);

        //swap(List list,int index1,int index2)
        Collections.swap(list,1,2);
        System.out.println(list);

        //int frequency(Collection,Object)
        int frequency = Collections.frequency(list, 22);
        System.out.println("frequency="+frequency);

        //void copy(List list,List src):将src中的内容赋值到list中(要保证list.size()>=src.size())
        //否则会抛IndexOutOfBoundsException("Source does not fit in dest")异常

        List src=new ArrayList();
        src.add(123);
        src.add(12);
        src.add(133);
        src.add(43);

        List list2= Arrays.asList(new Object[src.size()]);
        Collections.copy(list2,src);

        System.out.println(list2);

    }

    @Test
    public void test2(){

        List list=new ArrayList();
        list.add(123);
        list.add(122);
        list.add(22);
        list.add(67);

        //返回的list2即为线程安全的List
        List list2 = Collections.synchronizedList(list);

    }

}

```

# ***泛型***

```java
**
 * @author lycprimer
 * @create 2021-01-11 9:19
 * 泛型的使用：
 * JDK1.5新增特性
 *
 * 泛型的类型必须是类，不能是基本数据类型
 * 如果实例化时没有指明泛型，默认类型为java.lang.Object类型
 */
public class GenericTest {


    @Test
    public void test1(){

        ArrayList<Integer> list = new ArrayList<Integer>();

        //编译时就会进行类型检查，保证数据安全
        list.add(88);
        list.add(82);
        list.add(78);
        list.add(23);

        //避免了强转操作
        for(Integer score:list){

            int stuScore= score;
            System.out.println(stuScore);
        }

        Iterator<Integer> iterator = list.iterator();
        while(iterator.hasNext()){
            int stuScore=iterator.next();
            System.out.println(stuScore);
        }
    }

    @Test
    public void test2(){

        Map<String, Integer> map = new HashMap<String, Integer>();

        map.put("Tom",22);
        map.put("Jerry",14);
        map.put("Kitty",65);
        map.put("Simon",34);

        Set<Map.Entry<String, Integer>> entrySet = map.entrySet();
        Iterator<Map.Entry<String, Integer>> iterator = entrySet.iterator();
        while(iterator.hasNext()){
            Map.Entry<String, Integer> entry = iterator.next();
            String key = entry.getKey();
            Integer value = entry.getValue();
            System.out.println(key+"--->"+value);
        }

    }
}
```

## 自定义泛型类、接口、方法

```java
public class GenericClass<T> {

    String name;
    int Id;


    //类的内部结构就能使用类的泛型
    T classT;

    public GenericClass(){

    }

    public  void setClassT(T classT){
        this.classT=classT;
    }

    //静态方法中不能使用类的泛型
    //调用方式时可能类还没有实例化
    public static void show(){
        //System.out.println(classT);
    }

    @Test
    public void test1(){

        //如果定义了泛型类，实例化没有指明类的泛型，则认为此泛型类型为Object类型
        GenericClass gen=new GenericClass();
        gen.setClassT(123);
        gen.setClassT("abc");

        //如果定义了类是带泛型的，建议在实例化时指明类的泛型
        GenericClass<String> gen2=new GenericClass<String>();
        gen2.setClassT("apple");
        gen2.setClassT("banana");

        System.out.println(gen2.classT);

    }

    @Test
    public void test2(){

        subGenericClass sub=new subGenericClass();
        //由于子类在继承带泛型的父类时，指明了泛型类型。则实例化子类时，不需要再指明泛型
        //注意：此时subGenericClass不是泛型类，因此不能指明泛型类型
        sub.setClassT(123);
        System.out.println(sub.classT);

    }

    @Test
    public void test3(){
        //此时，subGenericClass2是泛型类，可以指明泛型类型
        subGenericClass2<String> sub2=new subGenericClass2<String>();
        sub2.setClassT("haha");
        System.out.println(sub2.classT);

    }

    @Test
    public void test4(){

        //泛型不同的引用不能相互赋值
        ArrayList<String> list1=null;
        ArrayList<Integer> list2=null;
    }

    //泛型方法：在方法中出现了泛型的结构，泛型参数与类的泛型参数没有任何关系
    //即，泛型方法所属的类是不是泛型类都没有关系
    //泛型方法可以声明为静态的。因为泛型参数是在调用方法时确定的，并非是在实例化时确定的
    //static后的尖括号是声明E是一个泛型，而非类名
    public static <E>  List<E> copyFromArrayToList(E[]arr){
//第一个<E>是为了声明E是泛型类而不是某一个自定义类
        ArrayList<E>list=new ArrayList<E>();
        for(E e:arr){
            list.add(e);
        }
        return list;
    }

    @Test
    public void test5(){
        //测试泛型方法
        Integer[]arr=new Integer[]{1,2,3,4};
        List<Integer>list=this.copyFromArrayToList(arr);
        System.out.println(list);
    }


}
class subGenericClass extends GenericClass<Integer>{

}

class subGenericClass2<T> extends GenericClass<T>{

}
```

```java
public class InheritGeneric {

    //虽然类A是类B的父类，但是G<A>和G<B>不具备子父类关系，二者是并列关系
    List<Object>list1=null;
    List<String>list2=null;
    //list1=list2; 编译报错
    //如果类A是类B的父类，A<G>与B<G>存在子父类关系


    //不能通过一个方法对List<Object>与List<String>进行操作
    public void show(List<Object> list){

    }
    public void show2(List<String> list){

    }


    //通配符的使用
    //通配符：?
    //类A是类B的父类，G<A>和G<B>是没有关系的，但二者共同的父类为G<?>
    @Test
    public void test1(){

        List<Object>list1=null;
        List<String>list2=null;

        List<?>list =null;

        list=list1;
        list=list2;

        //实现了通过一个方法同时操作List<Object>与List<String>
        print(list1);
        print(list2);


        List<String>list3=new ArrayList<>();
        list3.add("AA");
        list3.add("BB");
        list3.add("CC");

        list=list3;
        //对于List<?>就不能向其内部添加数据
        //除了添加null之外
        //list.add();
        list.add(null);
        Object o = list.get(0);

    }

    public void print(List<?>list){
        Iterator<?> iterator = list.iterator();
        while(iterator.hasNext()){
            Object obj = iterator.next();
            System.out.println(obj);
        }
    }

    @Test
    public void test2(){
        //有限制条件的通配符的使用：
        //  ? extends A:   G<? extends A>可以作为G<A>和G<B>的父类，其中B是A的子类
        //  ? super A:     G<? super A>可以作为G<A>和G<B>的父类，其中B是A的父类

        List<? extends Person>list1=null;
        List<? super Person>list2=null;

        List<Student> list3=null;
        List<Person>list4=null;
        List<Object>list5=null;

        list1=list3;
        list1=list4;
//      list1=list5; 编译报错

//      list2=list3; 编译报错
        list2=list4;
        list2=list5;

        list1=list3;
        Person p=list1.get(0);
        Student s=(Student)list1.get(0);

    }

}

class Person{

}
class Student extends Person{

}
```



# ***IO流***

## File类

```java
public class FileTest {

    @Test
    public void test1(){
        /*
        如何创建File类的实例
        File(String filePath)
        File(String parentPath,String childPath)
        File(File parentFile,String childPath)

        绝对路径：相较于某个路径下，指明的路径
        相对路径：包含盘符在内的文件或文件目录的路径

         */

        //构造器1
        File file1=new File("Hello.txt"); //相对于当前module

        File file2=new File("E:\\qycache\\JavaFile\\IDEACode\\JavaSenior\\IOStream\\src");

        System.out.println(file1);
        System.out.println(file2);

        //构造器2
        File file3=new File("E:\\qycache","JavaFile\\IDEACode");

        //构造器3
        File file4=new File(file3,"hi.txt");
    }

    @Test
    public void test2(){

        File file1=new File("Hello.txt");
        File file2=new File("E:\\qycache\\IO\\hi.txt");

        System.out.println(file1.getAbsoluteFile());//获取绝对路径
        System.out.println(file1.getPath());//获取路径
        System.out.println(file1.getName());//获取名称
        System.out.println(file1.getParent());//获取上层文件目录路径。若无，返回null
        System.out.println(file1.length());//返回文件长度（字节数）。不能获取目录长度
        System.out.println(new Date(file1.lastModified()));//获取最后一次修改时间(时间戳)

        System.out.println("******************************");

        System.out.println(file2.getAbsoluteFile());
        System.out.println(file2.getPath());
        System.out.println(file2.getName());
        System.out.println(file2.getParent());
        System.out.println(file2.length());
        System.out.println(file2.lastModified());
    }

    @Test
    public void test3(){
        //以下方法使用于文件目录
        File file=new File("D:\\Zero_Config_document");

        String[] list=file.list();   //获取文件目录下的文件与文件目录名
        for(String s:list){
            System.out.println(s);
        }
        System.out.println("*************************");
        File[]lists=file.listFiles(); //获取文件目录下的文件与文件目录
        for(File f:lists){
            System.out.println(f);
        }
    }

    @Test
    public void test4(){

        //public boolean renameTo(File dest):把文件重命名为指定的文件路径
        // file1.renameTo(file2):
        //要想保证返回true，需要file1在硬盘中是存在的，且file2不能在硬盘中存在
        File file1=new File("hello.txt");
        File file2=new File("E:\\qycache\\IO\\hi.txt");

        boolean renameTo = file1.renameTo(file2);
        System.out.println(renameTo);
    }

    @Test
    public void test5(){

        //判断是文件目录还是文件
        //public boolean isDirectory()
        //public boolean isFile()

        File file1=new File("helloworld.txt");
        System.out.println(file1.isFile());
        System.out.println(file1.isDirectory());
        System.out.println(file1.exists());
        System.out.println(file1.canRead());
        System.out.println(file1.canWrite());
        System.out.println(file1.isHidden());

        System.out.println("*******************************");

        file1=new File("E:\\qycache\\IO");
        System.out.println(file1.isFile());
        System.out.println(file1.isDirectory());
        System.out.println(file1.exists());
        System.out.println(file1.canRead());
        System.out.println(file1.canWrite());
        System.out.println(file1.isHidden());
    }

    @Test
    public void test6() throws IOException {
        /*
        创建硬盘中对应的文件或文件目录
        public boolean createNewFile():创建文件。若文件存在，则不创建，并返回false
        public boolean mkdir():创建文件目录。若此文件目录存在，则不创建，并返回false
        public boolean mkdirs():创建文件目录，若上层文件目录不存在，一并创建

        删除磁盘中的文件或文件目录
        public boolean delete()
        */
        File file1=new File("E:\\qycache\\haha.txt");
        if(!file1.exists()){
            file1.createNewFile();
            System.out.println("创建成功!");
        }else{
            file1.delete();
            System.out.println("删除成功!");
        }
    }

    @Test
    public void test7(){
        File file=new File("E:\\qycache\\hello");
        boolean mkdir = file.mkdir();
        if(mkdir){
            System.out.println("创建成功!");
        }

        File file2=new File("E:\\qycache\\Apple\\Banana");
        boolean mkdirs = file2.mkdirs();
        if (mkdirs){
            System.out.println("创建成功!");
        }
    }
}
```

## 流的体系架构

| 抽象基类     | 节点流(文件流)                                        | 缓冲流(处理流的一种)                                       |
| ------------ | ----------------------------------------------------- | ---------------------------------------------------------- |
| InputStream  | FileInputStream    read(byte[] buffer)    int         | BufferedInputStream    read(byte[] buffer)    int          |
| OutputStream | FileOutputStream   write(byte[] buffer,0,len)    void | BufferedOutputStream    write(byte[] buffer,0,len)    void |
| Reader       | FileReader    read(char[] cbuf)    int                | BufferedReader    read(char[] cbuf)    int/readLine()      |
| Writer       | FileWriter    write(char[] cbuf,0,len)    void        | BufferedWriter    write(char[] cbuf,0,len)    void         |

![](Java笔记.assets/IOStream.png)





## 节点流(文件流)

### 1.字符流(FileReader、FileWriter)

```java
public class FileReaderWriterTest {

    @Test
    public void test1() {
        /*
        将hello.txt文件内容读入程序中，并输出到控制台
        read()方法：返回读入的一个字符，如果到达文件末尾，返回-1
        异常处理：为保证流资源一定可以执行关闭操作，需要使用try-catch-finally处理，而不要抛出异常
        读入的文件一定要存在，否则会报FileNotFoundException

         */
        FileReader fr= null;

        try {
            //1.实例化File类的对象，指明要操作的文件
            File file=new File("hello.txt");    //相较于当前Module

            //2.提供具体的流
            fr = new FileReader(file);

            //3.数据读入
            //read()方法：返回读入的一个字符，如果到达文件末尾，返回-1
            int data=fr.read();
            while(data!=-1){
                System.out.print((char)data);
                data=fr.read();
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //流的关闭操作
            try {
                if(fr!=null) {
                    fr.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }


    //对read()方法操作升级：使用read()的重载方法
    @Test
    public void test2() throws IOException {

        //1.File类的实例化
        File file=new File("hello.txt");
        //2.FileReader流的实例化
        FileReader fr=new FileReader(file);
        //3.读入操作read(char[]cbuf)：返回值为每次读入cbuf数组中的字符个数。如果到达末尾，返回-1
        char [] cbuf=new char[5];
        int length;
        length=fr.read(cbuf);
        while(length!=-1){
            for(int i=0;i<length;i++){  //注意不能写i<cbuf.length，否则结果为HelloWorld!!!ld
                System.out.print(cbuf[i]);
            }
            length=fr.read(cbuf);
        }
        //4.资源的关闭
        fr.close();
    }


    //从内存中写出数据到硬盘的文件中FileWriter(file)/FileWriter(file,false)/FileWriter(file,true)
    @Test
    public void test3() throws IOException {

        /*
        输出操作：对应的File可以不存在，在输出的过程中会自动创建此文件
                 如果存在：如果流使用的构造器是FileWriter(file,false)/FileWriter(file):对原有文件进行覆盖
                          如果流使用的构造器是FileWriter(file,true)：不会对原有文件进行覆盖，而是追加内容


         */
        //1.提供File类的对象，指明写出到的文件
        File file=new File("hello2.txt");

        //2.提供FileWriter的流对象，用于数据的写出
        FileWriter fw=new FileWriter(file,true);

        //3.写出操作
        fw.write("I have a dream!\n");
        fw.write("You need to have a dream!");

        //资源关闭
        fw.close();

    }

    @Test
    public void test4()   {
        FileReader fr= null;
        FileWriter fw= null;

        try {
            //创建File类的对象，指明读入和写出的文件
            File srcFile=new File("hello.txt");
            File destFile=new File("hello3.txt");

            //创建输入流和输出流对象
            fr = new FileReader(srcFile);
            fw = new FileWriter(destFile);

            //数据的读入和写出操作
            char[]cbuf=new char[5];
            int len;//记录每次读入到cbuf数组中的字符的个数
            while((len=fr.read(cbuf))!=-1){
                //每次写出len个字符
                fw.write(cbuf,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //关闭流资源
            try {
                fw.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                fr.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }

    }

}
```

### 2.字节流(FileInputStream、FileOutputStream)

```java
/**
 * @author lycprimer
 * @create 2021-01-12 17:19
 *
 * 对于文本文件(.txt,.java,.cpp)使用字符流处理
 * 对于非文本文件(.jpg,.png,.mp4,.avi,.doc,.ppt)使用字节流处理
 
 * 对于文本文件的复制操作而言，也可以使用字节流，但是在内存层面会出现中文乱码，复制完成后，
   在存储层面不会出现乱码。
 
 * 但是，非文本文件的复制复制操作不能使用字符流
 */
public class FileInputOutputTest {

    @Test
    public void test1() {

        FileInputStream fis= null;
        try {
            File file =new File("hello.txt");

            fis = new FileInputStream(file);

            byte[]buffer=new byte[5];
            int len;
            while((len=fis.read(buffer))!=-1){
                String str=new String(buffer,0,len);
                System.out.print(str);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                fis.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

    //通过字节流复制图片
    @Test
    public void test2() {

        FileInputStream fi= null;
        FileOutputStream fo= null;
        try {
            File file=new File("E:\\qycache\\IDEA.png");
            File toFile=new File("picture.png");

            fi = new FileInputStream(file);
            fo = new FileOutputStream(toFile);

            byte[]buffer=new byte[1024];
            int len;
            while((len=fi.read(buffer))!=-1){
                fo.write(buffer,0,len);
            }

        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            try {
                fi.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                fo.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
```

## 缓冲流(处理流的一种)

```java
/**
 * @author lycprimer
 * @create 2021-01-12 18:08
 *
 * 缓冲流的使用：
 *
 * 缓冲流(处理流的一种)
 * BufferedInputStream
 * BufferedOutputStream
 * BufferedReader
 * BufferedWriter
 *
 * 处理流就是“套接”在已有的流的基础上
 *
 * 作用：提升流的读取、写入速度
 * 提高读写速度原因：内部提供了一个缓冲区
 *
 *
 */
public class BufferedTest {

    //实现非文本文件复制
    @Test
    public void test1() throws FileNotFoundException {

        BufferedInputStream bis= null;
        BufferedOutputStream bos= null;
        try {
            File srcFile=new File("E:\\qycache\\HerSchool.mp4");
            File toFile=new File("E:\\qycache\\JavaFile\\HerSchool.mp4");

            //字节流
            FileInputStream fis=new FileInputStream(srcFile);
            FileOutputStream fos=new FileOutputStream(toFile);

            //缓冲流
            bis = new BufferedInputStream(fis);
            bos = new BufferedOutputStream(fos);

            //复制细节：读取、写入
            byte[]buffer=new byte[1024];
            int len;
            while((len=bis.read(buffer))!=-1){
                bos.write(buffer,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //资源关闭(先关闭外层的流，在关闭内层的流)
            //在关闭外层流的同时，内层流也会自动关闭，内层流的关闭代码可省略
            try {
                if (bos!=null) {
                    bos.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                if (bis!=null) {
                    bis.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

    @Test
    public void test2(){
        long start=System.currentTimeMillis();

        copyFile("E:\\qycache\\HerSchool.mp4","E:\\qycache\\JavaFile\\HerSchool.mp4");

        long end=System.currentTimeMillis();
        System.out.println("耗时: "+(end-start)+" ms");
    }


    public void copyFile(String src,String target){

        BufferedInputStream bis= null;
        BufferedOutputStream bos= null;
        try {
            File srcFile=new File(src);
            File toFile=new File(target);

            //字节流
            FileInputStream fis=new FileInputStream(srcFile);
            FileOutputStream fos=new FileOutputStream(toFile);

            //缓冲流
            bis = new BufferedInputStream(fis);
            bos = new BufferedOutputStream(fos);

            //复制细节：读取、写入
            byte[]buffer=new byte[1024];
            int len;
            while((len=bis.read(buffer))!=-1){
                bos.write(buffer,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //资源关闭(先关闭外层的流，在关闭内层的流)
            //在关闭外层流的同时，内层流也会自动关闭，内层流的关闭代码可省略
            try {
                if (bos!=null) {
                    bos.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                if (bis!=null) {
                    bis.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }


    //使用BufferedReader和BufferedWriter实现文本文件的复制
    @Test
    public void test3(){
        BufferedReader br= null;
        BufferedWriter bw= null;

        try {
            //造文件，造节点流，造缓冲流
            br = new BufferedReader(new FileReader(new File("copySrc.txt")));
            bw = new BufferedWriter(new FileWriter(new File("E:\\qycache\\copyVersion.txt")));

            //读写操作

            //方式一：
//            char[]cbuf=new char[16];
//            int len;
//            while((len=br.read(cbuf))!=-1){
//                bw.write(cbuf,0,len);
//            }

            //方式二：(缓冲流特有)
            String data;
            while((data=br.readLine())!=null){
                bw.write(data);//data中不包括换行符
                bw.write("\n"); //手动添加换行符，也可以调用bw.newLine()方法
            }

        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //关闭资源
            try {
                if (bw!=null) {
                    bw.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
            try {
                if (br!=null) {
                    br.close();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }

        }


    }
}
```

## 转换流(处理流的一种)

```java
/**
 * @author lycprimer
 * @create 2021-01-13 10:12
 *
 * 转换流：属于字符流，也是处理流
 *   InputStreamReader：将一个字节的输入流转换为字符的输入流
 *   OutputStreamWriter：将一个字符的输出流转换为字节的输出流
 * 作用：提供字节流与字符流之间的转换
 */
public class InputStreamReaderTest {

    @Test
    public void test1(){

        InputStreamReader isr= null;
        try {
            FileInputStream fis=new FileInputStream("hello.txt");
            //InputStreamReader isr=new InputStreamReader(fis);//使用系统默认的字符集UTF-8
            //参数2指明了字符集，具体使用的字符集取决于文件保存时使用的字符集
            isr = new InputStreamReader(fis,"UTF-8");

            char[] cbuf=new char[20];
            int len;
            while((len=isr.read(cbuf))!=-1){

                String str=new String(cbuf,0,len);
                System.out.print(str);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(isr!=null){
                try {
                    isr.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    //综合使用InputStreamRead与OutputStreamWriter
    //读入utf-8格式的文本文件，输出gbk格式的文本文件
    @Test
    public void test2(){

        InputStreamReader isr= null;
        OutputStreamWriter osw= null;
        try {
            File file1=new File("hello.txt");
            File file2=new File("E:\\qycache\\foryou.txt");

            FileInputStream fis=new FileInputStream(file1);
            FileOutputStream fos=new FileOutputStream(file2);

            isr = new InputStreamReader(fis,"UTF-8");
            osw = new OutputStreamWriter(fos,"GBK");

            char[]cbuf=new char[5];
            int len;
            while((len=isr.read(cbuf))!=-1){
                osw.write(cbuf,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(isr!=null){
                try {
                    isr.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(osw!=null){
                try {
                    osw.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
//注意：要先关闭转化流，之后再关闭节点流！！！！！！！
```

## 标准输入、输出流

```java
/**
 * @author lycprimer
 * @create 2021-01-13 11:29
 *
 * 其他流的使用：
 * 1.标准输入、输出流
 * 2.打印流
 * 3.数据流
 */
public class OtherStreamTest {


    @Test
    public void test1(){
        /**
         * 标准输入、输出流：
         * System.in:标准输入流，默认从键盘输入
         * System.out:标准输出流，默认从控制台输出
         *
         * System类的setIn(InputStream is)/setOut(OutputStream ps)方法重写指定输入和输出的流
         *
         * 练习：从键盘输入字符串，将读取到的整行字符串转换成大写输出，然后继续进行输入操作
         *      直到输入‘e’或‘exit’时，退出程序
         *
         * 方法一：通过Scanner实现，调用next()方法，返回一个字符串
         * 方法二：通过System.in实现，System.in--->转换流--->BufferedReader的readLine()方法
         *        (因为BufferedReader特有readLine()方法，所以才需要转换流)
         */

        BufferedReader br= null;
        try {
            InputStreamReader isr=new InputStreamReader(System.in);//System.in为字节流

            br = new BufferedReader(isr);

            while(true){
                System.out.println("请输入字符串");
                String data=br.readLine();
                if(data.equalsIgnoreCase("e")||data.equalsIgnoreCase("exit")){
                    System.out.println("程序结束");
                    break;
                }
                String upperCase = data.toUpperCase();
                System.out.println(upperCase);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(br!=null){
                try {
                    br.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }


    }
}
```

## 打印流

```java
@Test
    public void test2(){
        PrintStream ps =null;
        try {
            FileOutputStream fos=new FileOutputStream(new File("E:\\qycache\\char.txt"));
            ps = new PrintStream(fos, true);
            if(ps!=null){//把标准输出流(控制台输出)改成输出到文件
                System.setOut(ps);
            }

            //打印256种字符
            for(int i=0;i<255;i++){
                System.out.print((char)i);
                if(i%50==0){
                    System.out.println();
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            ps.close();
        }
    }
```

## 数据流

```java
@Test
    public void test3() {
        /**
         * 数据流：
         * DataInputStream和DataOutputStream
         * 作用：用于读取或写入基本数据类型的变量或字符串
         * 练习：将内存中的字符串、基本数据类型的变量写出到文件中
         */

        DataOutputStream dos= null;
        try {
            dos = new DataOutputStream(new FileOutputStream(new File("E:\\qycache\\data.txt")));
            dos.writeUTF("霍建华");
            dos.flush();    //刷新，将内存中的数据写入文件
            dos.writeInt(34);
            dos.flush();
            dos.writeBoolean(true);
            dos.flush();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(dos!=null){
                try {
                    dos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    @Test
    public void test4(){
        /**
         * 注意：读取不同类型的数据的顺序要与当初写入文件时，保持数据的顺序一致
         */
        DataInputStream dis= null;
        try {
            dis = new DataInputStream(new FileInputStream(new File("E:\\qycache\\data.txt")));

            String name = dis.readUTF();
            int age = dis.readInt();
            boolean isMale = dis.readBoolean();

            System.out.println("name = "+name);
            System.out.println("age = "+age);
            System.out.println("isMale = "+isMale);
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(dis!=null){
                try {
                    dis.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
```

## 对象流

```java
/**
 * @author lycprimer
 * @create 2021-01-13 16:25
 *
 * 对象流的使用：
 * ObjectInputStream
 * ObjectOutputStream
 *
 * 作用：用于存储和读取基本数据类型或对象的处理流
 *
 * 要想一个java对象是可序列化的，需要满足相应要求
 *      例：Person需要满足如下要求:
 *          1.实现Serializable接口
 *          2.需要当前类提供一个全局常量(public static final long):serialVersionUID序列版本号
 *          3.除了当前Person类是需要实现Serializable接口之外，还要保证其内部所有属性也必须是可序列化的
 *            (默认情况下，基本数据类型是可序列化的)
 *
 *
 * 补充：ObjectOutputStream和ObjectInputStream不能序列化static和transient修饰的成员变量
 */
public class ObjectStream {


    @Test
    public void test1(){
        /**
         * 序列化过程：将内存中的java对象保存到磁盘中或通过网络传输出去
         * 使用ObjectOutputStream实现
         */
        ObjectOutputStream oos= null;
        try {
            oos = new ObjectOutputStream(new FileOutputStream(new File("E:\\qycache\\object.dat")));
            oos.writeObject(new String("我是中国人"));
            oos.flush();//刷新操作

            oos.writeObject(new Person("孙悟空",999,new Account(10010,2000)));
            oos.flush();
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(oos!=null){
                try {
                    oos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
//注意：序列化顺序要与反序列化顺序一致，即若序列化顺序为Person类、String类，那么，反序列化顺序也应为Person类、String类
    @Test
    public void test2(){
        /**
         * 反序列化过程：将磁盘文件中的对象还原为内存中的一个java对象
         * 使用ObjectInputStream实现
         */

        ObjectInputStream ois= null;
        try {
            ois = new ObjectInputStream(new FileInputStream(new File("E:\\qycache\\object.dat")));
            Object obj=ois.readObject();
            String str=(String)obj;

            Person p=(Person)ois.readObject();

            System.out.println(str);
            System.out.println(p);
        } catch (IOException e) {
            e.printStackTrace();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } finally {
            if(ois!=null){
                try {
                    ois.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
class Person implements Serializable{
    private String name;
    private int age;
    private Account acct=new Account();
    public static final long serialVersionUID=6763558489758302169L;

    public Person() {
    }

    public Person(String name, int age, Account acct) {
        this.name = name;
        this.age = age;
        this.acct = acct;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public Account getAcct() {
        return acct;
    }

    public void setAcct(Account acct) {
        this.acct = acct;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", acct=" + acct +
                '}';
    }
}

class Account implements  Serializable{
    private int Id;
    private double balance;
    public static final long serialVersionUID=2343523576387563L;

    public Account(int id, double balance) {
        Id = id;
        this.balance = balance;
    }

    public Account() {
    }

    public int getId() {
        return Id;
    }

    public void setId(int id) {
        Id = id;
    }

    public double getBalance() {
        return balance;
    }

    public void setBalance(double balance) {
        this.balance = balance;
    }

    @Override
    public String toString() {
        return "Account{" +
                "Id=" + Id +
                ", balance=" + balance +
                '}';
    }
}
```

## 任意存取文件流

```java
/**
 * @author lycprimer
 * @create 2021-01-13 17:15
 * RandomAccessFile类的使用：
 *
 * RandomAccessFile类直接继承于java.lang.Object类，实现了DataInput和DataOutput接口
 * RandomAccessFile既可以作为输入流，也可以作为输出流
 *
 *如果RandomAccessFile作为输出流时，写出到的文件不存在，则在执行过程中自动创建
 * 如果写出到的文件存在，则默认情况下，会对原有文件内容进行从头覆盖(区别于完全覆盖！)
 *
 * 可以通过相关操作实现"插入"效果(注意指针在不断移动)
 *
 */
public class RandomAccessFileTest {

    @Test
    public void test1(){

        RandomAccessFile raf1= null;
        RandomAccessFile raf2= null;
        try {
            raf1 = new RandomAccessFile(new File("E:\\qycache\\Tasks.txt"),"r");
            raf2 = new RandomAccessFile(new File("E:\\qycache\\TasksVersion.txt"),"rw");

            byte[]buffer=new byte[4];
            int len;
            while ((len=raf1.read(buffer))!=-1){

                raf2.write(buffer,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(raf1!=null){
                try {
                    raf1.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(raf2!=null){
                try {
                    raf2.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }

    @Test
    public void test2() throws IOException {

        RandomAccessFile raf = new RandomAccessFile(new File("characterTest.txt"), "rw");
        raf.seek(new File("characterTest.txt").length());//将指针调到文件末尾的位置
        raf.write("xyz".getBytes());

        raf.close();
    }

    @Test
    public void test3() throws IOException {
        /**
         * 使用RandomAccessFile实现数据的插入效果
         * 理解：再读取或写入的过程中，seek()所操作的那个指针也在不断移动
         */
        RandomAccessFile raf = new RandomAccessFile(new File("characterTest.txt"), "rw");
        raf.seek(3);//指针移至3处，读取的时候也是从3处开始读取

        //保存指针3后面的所有数据
        StringBuilder builder=new StringBuilder((int) new File("characterTest.txt").length());
        byte[]buffer=new byte[20];
        int len;
        while((len=raf.read(buffer))!=-1){
            builder.append(new String(buffer,0,len));
        }
        //调回指针，写入"xyz"
        raf.seek(3);
        raf.write("xyz".getBytes());

        //将StringBuilder中的数据写入到文件中
        raf.write(builder.toString().getBytes());

        raf.close();
    }
}
```





# ***网络编程***



## InetAddress类

```java
/**
 * @author lycprimer
 * @create 2021-01-14 10:56
 *
 * IP:唯一的标识Internet上的通信实体
 * 在Java中使用InetAddress类代表IP
 * IP分类：IPv4和IPv6；万维网 和 局域网
 * 本地回路地址：127.0.0.1对应着localhost
 *
 * 如何实例化InetAddress：getByName(String host)、getLocalHost()
 * 常用方法：getHostName()/getHostAddress()
 *
 * 端口号：正在计算机上运行的进程
 * 要求：不同的进程有不同的端口号
 *
 * 端口号与IP地址的组合得出一个网络套接字：Socket
 *
 */
public class InetAddressTest {

    public static void main(String[] args) throws UnknownHostException {

        InetAddress inet1 = InetAddress.getByName("192.168.10.14");
        System.out.println(inet1);

        InetAddress inet2= InetAddress.getByName("www.baidu.com");
        System.out.println(inet2);

        InetAddress inet3= InetAddress.getByName("127.0.0.1");//本地IP
        System.out.println(inet3);

        //获取本机IP
        InetAddress inet4=InetAddress.getLocalHost();
        System.out.println(inet4);

        System.out.println(inet4.getHostName());
        System.out.println(inet4.getHostAddress());
    }
}
```

## TCP/IP网络编程

### (1)例1：

```java
/**
 * @author lycprimer
 * @create 2021-01-14 11:59
 * 实现TCP的网络编程
 *
 * 例1：客户端发送信息给服务端，服务端将数据显示在控制台上
 
理解Socket网络套件：
Socket网络套件是一条船，其构造器形参列表指明了其目的地(IP地址与端口号)，小船上有OutputStream用于装配出口货物

ServeSocket网络套件是目的地的工作台，它的构造器形参声明了自己所处港口的名称(断口号)，无需声明自己的IP地址
通过accept()方法接收外来小船，并生成一个自己的小船，生成的小船可通过InputStream获取穿上的进口货物


 */
public class TCPTest {

    //客户端
    @Test
    public void client(){
        Socket socket= null;
        OutputStream os= null;
        try {
            //1.创建Socket对象，指明服务器端的IP和端口号
            InetAddress inet=InetAddress.getByName("127.0.0.1");
            socket = new Socket(inet,8899);
            //2.获取一个输出流，用于输出数据
            os = socket.getOutputStream();
            //3.写出数据
            os.write("你好，我是客户端".getBytes());
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //4.资源关闭
            if(os!=null){
                try {
                    os.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(socket!=null){
                try {
                    socket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }

    }

    //服务器端
    @Test
    public void server() {

        ServerSocket serverSocket = null;
        Socket accept = null;
        InputStream is = null;
        InputStreamReader isr= null;
        try {
            //1.创建服务器端的ServerSocket，指明自己的端口号
            serverSocket = new ServerSocket(8899);
            //2.调用accept()方法，接受来自客户端的socket
            accept = serverSocket.accept();
            //3.获取输入流
            is = accept.getInputStream();
            //4.读取输入流中的数据
            isr = new InputStreamReader(is);
            char[]cbuf=new char[5];
            int len;
            StringBuilder sb=new StringBuilder();
            while((len=isr.read(cbuf))!=-1){
                sb.append(new String(cbuf,0,len));
            }

            System.out.println(sb);
            System.out.println("收到了来自于："+accept.getInetAddress().getHostAddress()+" 的数据");

        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            //5.资源关闭
            if(isr!=null){
                try {
                    isr.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(is!=null){
                try {
                    is.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(accept!=null){
                try {
                    accept.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(serverSocket!=null){
                try {
                    serverSocket.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

### (2)例2：

```java
/**
 * @author lycprimer
 * @create 2021-01-14 15:15
 *
 * 例2：客户端发送文件给服务器，服务器将文件保存在本地
 * 涉及到的异常应该使用try-catch-finally处理
 */
public class TCPTest2 {
    @Test
    public void client() throws IOException {

        Socket socket=new Socket(InetAddress.getByName("127.0.0.1"),9090);

        OutputStream os = socket.getOutputStream();

        FileInputStream fis=new FileInputStream(new File("E:\\qycache\\client\\IOStream.png"));
        byte[]buffer=new byte[1024];
        int len;
        while((len=fis.read(buffer))!=-1){
            os.write(buffer,0,len);
        }

        fis.close();
        os.close();
        socket.close();
    }

    @Test
    public void server() throws IOException {

        ServerSocket serverSocket = new ServerSocket(9090);

        Socket accept = serverSocket.accept();

        InputStream is = accept.getInputStream();

        FileOutputStream fos=new FileOutputStream(new File("E:\\qycache\\server\\acceptVersion.png"));

        byte[]buffer=new byte[1024];
        int len;
        while((len=is.read(buffer))!=-1){
            fos.write(buffer,0,len);
        }

        fos.close();
        is.close();
        accept.close();


    }

}
```

### (3)例3：

```java
/**
 * @author lycprimer
 * @create 2021-01-14 15:27
 *
 * 例3：从客户端发送文件给服务器，服务器保存到本地，并返回“发送成功”给客户端，并关闭链接
 */
public class TCPTest3 {

    @Test
    public void client() throws IOException {

        Socket socket=new Socket(InetAddress.getByName("127.0.0.1"),9090);

        OutputStream os = socket.getOutputStream();

        FileInputStream fis=new FileInputStream(new File("E:\\qycache\\client\\IOStream.png"));
        byte[]buffer=new byte[1024];
        int len;
        while((len=fis.read(buffer))!=-1){
            os.write(buffer,0,len);
        }
        //关闭数据输出
        socket.shutdownOutput();
        //例2之所以不用关闭是因为read()方法执行完就会close链接。但是对于本例，read()方法执行完会等待服务器反馈，无法close连接。而对于服务器，其read()方法因为不是对文件进行操作，无法得知结束标志，只有当客户端close链接时，才会执行完read()方法(read()方法是一种阻塞方法)。因此，在本例中，要手动关闭数据输出
        

        //接收来自服务器的反馈
        //可以理解为小船已经返航，此时客户端要从返航的小船上提取出输出流，得到服务器反馈
        InputStream is = socket.getInputStream();
        StringBuilder sb=new StringBuilder();
        while((len=is.read(buffer))!=-1){
            sb.append(new String(buffer,0,len));
        }

        System.out.println(sb);

        fis.close();
        os.close();
        socket.close();
        is.close();
    }

    @Test
    public void server() throws IOException {

        ServerSocket serverSocket = new ServerSocket(9090);

        Socket accept = serverSocket.accept();

        InputStream is = accept.getInputStream();

        FileOutputStream fos=new FileOutputStream(new File("E:\\qycache\\server\\acceptVersion.png"));

        byte[]buffer=new byte[1024];
        int len;
        while((len=is.read(buffer))!=-1){
            fos.write(buffer,0,len);
        }

        //服务器给予客户端返回
        OutputStream os = accept.getOutputStream();
        os.write("服务器提示：图片发送成功！".getBytes());


        fos.close();
        is.close();
        accept.close();
        os.close();


    }
}
```



## UDP网络编程(了解)

```java
/**
 * @author lycprimer
 * @create 2021-01-14 16:03
 *
 * UDP协议的网络编程
 */
public class UDPTest {

    //发送端
    @Test
    public void send() throws IOException {

        DatagramSocket socket = new DatagramSocket();

        String str="我是UPD方式发送的导弹";
        byte[] data = str.getBytes();
        InetAddress inet=InetAddress.getLocalHost();
        DatagramPacket packet = new DatagramPacket(data,0,data.length,inet,9090);

        socket.send(packet);

        socket.close();

    }

    //接受端
    @Test
    public void receiver() throws IOException {

        DatagramSocket socket = new DatagramSocket(9090);
        byte[]buffer=new byte[100];

        DatagramPacket packet = new DatagramPacket(buffer,0,buffer.length);
        socket.receive(packet);

        System.out.println(new String(packet.getData(),0,packet.getLength()));

    }
}
```



## URL网络编程

```java
/**
 * @author lycprimer
 * @create 2021-01-14 16:22
 *
 * URL网络编程
 * URL：统一资源定位符，对应着互联网的某一资源地址
 * 格式：
 * http://localhost:8080/examples/beauty.jpg?username=Tom
 * 协议     主机名  端口号      资源地址          参数列表
 */
public class URLTest {

    public static void main(String[] args){

        HttpURLConnection urlConnection = null;
        InputStream is = null;
        FileOutputStream fos= null;
        try {
            URL url=new URL("https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fbpic.588ku.com%2Felement_origin_min_pic%2F16%2F08%2F25%2F2157bef46fc7618.jpg&refer=http%3A%2F%2Fbpic.588ku.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1613204911&t=9f3c571a18ba9bd7156e87fa03e69cb2");

            urlConnection = (HttpURLConnection) url.openConnection();

            urlConnection.connect();

            is = urlConnection.getInputStream();

            fos = new FileOutputStream(new File("E:\\qycache\\train.jpg"));

            byte[]buffer=new byte[1024];
            int len;
            while((len=is.read(buffer))!=-1){
                fos.write(buffer,0,len);
            }
        } catch (IOException e) {
            e.printStackTrace();
        } finally {
            if(is!=null){
                try {
                    is.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(fos!=null){
                try {
                    fos.close();
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
            if(urlConnection!=null){
                urlConnection.disconnect();
            }
        }
    }
}
```





# ***反射***

```java
/**
 * @author lycprimer
 * @create 2021-01-15 10:59
 *
 *关于java.lang.Class类的理解：
 * 1.类的加载过程：
 * 程序javac.exe命令以后，会生成一个或多个字节码文件(.class)，接着使用java.exe命令
 * 对某个字节码文件进行解释运行。相当于将某个字节码文件加载到内存中。此过程即为类的加载。
 * 加载到内存中的类，成为运行时类，此运行时类，就作为Class类的一个实例
 *
 * 也就是说，Class类的实例就对应着一个运行时类
 * 加载到内存中的运行时类，会缓存一段时间。在此时间内，可以通过不同的方式来获取此运行时类
 *
 对于私有的结构(属性、方法、构造器)，通过反射调用或修改时，首先要指定setAccessible(true)
 对于公有结构则不需要
 */
public class ReflectionTest {

    //反射之前对于Person类的操作
    @Test
    public void test1(){

        Person p1=new Person("Tom",12);

        p1.age=10;
        System.out.println(p1);

        p1.show();

        //在Person类的外部，不可以通过Person类的对象调用其内部的私有结构
    }

    //反射之后对于Person类的操作
    @Test
    public void test2() throws Exception{

        //通过反射，创建Person类的对象
        Class clazz = Person.class;
        Constructor cons = clazz.getConstructor(String.class, int.class);

        Object obj = cons.newInstance("Tom", 12);
        Person p=(Person) obj;
        System.out.println(p.toString());

        //通过反射，调用对象指定的属性、方法
        Field age = clazz.getDeclaredField("age");
        age.set(p,10);

        System.out.println(p.toString());

        //通过反射调用方法
        Method show = clazz.getDeclaredMethod("show");//调用空参show方法,若方法有参数，要写参数所属的类！
        show.invoke(p);

        //通过反射可以调用Person类的私有结构
        //调用私有构造器
        Constructor cons2 = clazz.getDeclaredConstructor(String.class);
        cons2.setAccessible(true);
        Object p2 = cons2.newInstance("Jerry");
        System.out.println(p2.toString());

        //调用私有属性
        Field name = clazz.getDeclaredField("name");
        name.setAccessible(true);
        name.set(p2,"Kitty");
        System.out.println(p2);

        //调用私有方法
        Method showNation = clazz.getDeclaredMethod("showNation", String.class);
        showNation.setAccessible(true);
        String nation=(String)showNation.invoke(p2,"China");//相当于String nation=p2.showNation("China");
        System.out.println(nation);

    }


    //获取Class实例的方式(前三个需要掌握)
    @Test
    public void test3() throws ClassNotFoundException {

        //方式一：调用运行时类的属性：.class
        Class<Person> clazz1 = Person.class;
        System.out.println(clazz1);

        //方式二：通过运行时类的对象
        Person p=new Person();
        Class<? extends Person> clazz2 = p.getClass();
        System.out.println(clazz2);

        //方式三：调用Class的静态方法：forName(String classPath)
        Class<?> clazz3 = Class.forName("Person");//注意，字符串内需要指定包名
        System.out.println(clazz3);

        System.out.println(clazz1==clazz2);//true
        System.out.println(clazz1==clazz3);//true

        //方式四：使用类的加载器：ClassLoader  (了解)
        ClassLoader classLoader = ReflectionTest.class.getClassLoader();
        Class<?> clazz4 = classLoader.loadClass("Person");

        System.out.println(clazz4);
        System.out.println(clazz1==clazz4);//true

    }

    @Test
    public void test4(){

        Class c1=Object.class;
        Class c2=Comparable.class;
        Class c3=String[].class;
        Class c4=int[][].class;
        Class c5= ElementType.class;
        Class c6=Override.class;
        Class c7=int.class;
        Class c8=void.class;
        Class c9=Class.class;

        int[]a=new int[10];
        int[]b=new int[100];

        Class c10=a.getClass();
        Class c11=b.getClass();

        //只要数组的元素类型与维度一样，就是同一个Class
        System.out.println(c10==c11);
    }

    @Test
    public void test5() throws Exception {

        Properties pros=new Properties();
        //此时的文件默认识别为在当前的module下
        //读取配置文件方式一：
//        FileInputStream fis=new FileInputStream("jdbc.properties");
//        pros.load(fis);

        //读取配置文件的方式二：
        //配置文件默认识别为当前module的src下
        ClassLoader classLoader = ReflectionTest.class.getClassLoader();
        InputStream is = classLoader.getResourceAsStream("jdbc.properties");
        pros.load(is);

        String user = pros.getProperty("user");
        String password = pros.getProperty("password");

        System.out.println("user="+user+",password="+password);
    }

}

class Person{
    private String name;
    public int age;

    public Person() {
        System.out.println("空参构造器调用");
    }

    private Person(String name){
        this.name=name;
    }

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public void show(){
        System.out.println("I am a person");
    }

    private String showNation(String nation){

        System.out.println("My country is "+nation);
        return nation;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```



```java
/**
 * @author lycprimer
 * @create 2021-01-15 14:59
 *
 * 通过反射创建对应的运行时类的对象
 */
public class NewInstanceTest {

    @Test
    public void test1() throws IllegalAccessException, InstantiationException {

        Class<Person> clazz=Person.class;
        /**
         * newInstance():调用此方法，创建对应的运行时类的对象，内部调用了运行时类的空参构造器
         *               若没有空参构造器，会抛InstantiationException
         *               若空参构造器过小，会抛IllegalAccessException
         *
         * 在javabean中要求提供一个public的空参构造器
         * 1.便于通过反射，创建运行时类的对象
         * 2.便于子类继承此运行时类时，默认调用super()时，保证父类有此构造器
         */
        Person person = clazz.newInstance();

        System.out.println(person);
    }


    //反射的动态性：在运行之前，无法确定创建的对象应该属于哪个类
    //只有运行时才能确定应该创建哪个类的对象
    @Test
    public void test2(){
        int num = new Random().nextInt(3);//产生0,1,2随机数
        String classPath="
            ";
        switch(num){
            case 0:
                classPath="java.util.Date";
                break;
            case 1:
                classPath="java.lang.Object";
                break;
            case 2:
                classPath="Person";
                break;
        }
        try {
            Object obj = getInstance(classPath);
            System.out.println(obj);
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InstantiationException e) {
            e.printStackTrace();
        }

    }

    /**
     * 创建一个指定类的对象
     * classPath:指定类的全类名
     */
    public Object getInstance(String classPath) throws ClassNotFoundException, IllegalAccessException, InstantiationException {

        Class<?> clazz = Class.forName(classPath);
        return clazz.newInstance();
    }
}
```



```java
public class PersonsTest {

    @Test
    public void FiledTest(){

        Class<Persons> clazz = Persons.class;

        //获取属性结构
        //getFields()方法：获取当前运行时类及其父类中声明为public访问权限的属性
        Field[] fields = clazz.getFields();

        for(Field f:fields){
            System.out.println(f);
        }

        System.out.println();

        //getDeclaredFields()方法：获取当前运行时类中声明的所有属性(不包含父类中声明的属性)
        Field[] declaredFields = clazz.getDeclaredFields();

        for(Field f:declaredFields){
            System.out.println(f);
        }

    }


    //获取属性修饰符、属性数据类型及变量名
    //权限修饰符   数据类型   变量名
    @Test
    public void test1(){

        Class<Person> clazz = Person.class;

        Field[] declaredFields = clazz.getDeclaredFields();

        for(Field f:declaredFields){

            //权限修饰符
            int modifiers = f.getModifiers();
            System.out.print(Modifier.toString(modifiers)+"\t");

            //数据类型
            Class<?> type = f.getType();
            System.out.print(type.getName()+"\t");

            //变量名
            String fName=f.getName();
            System.out.println(fName);

        }
    }


    //获取运行时类的方法结构
    @Test
    public void MethodTest(){

        Class<Persons> clazz = Persons.class;

        //getMethods()方法：获取当前运行时类及其所有父类中声明为public权限的方法
        Method[] methods = clazz.getMethods();

        for(Method m:methods){
            System.out.println(m);
        }

        System.out.println();

        //getDeclaredMethods()：获取当前运行时类中声明的所有方法(不包含父类中声明的方法)
        Method[] declaredMethods = clazz.getDeclaredMethods();
        for(Method m:declaredMethods){
            System.out.println(m);
        }
    }

    //权限修饰符   返回值类型   方法名(参数类型1 形参名1，...) throws xxxException
    @Test
    public void test2(){

        Class<Persons> clazz = Persons.class;
        Method[] methods = clazz.getMethods();
        for(Method m:methods){

            //权限修斯符
            System.out.print(Modifier.toString(m.getModifiers())+"\t");

            //返回值类型
            System.out.print(m.getReturnType().getName()+"\t");

            //方法名
            System.out.print(m.getName());

            System.out.print("(");
            //形参列表
            Class<?>[] parameterTypes = m.getParameterTypes();
            if(!(parameterTypes==null&&parameterTypes.length==0)){
                for(int i=0;i<parameterTypes.length;i++){
                    if(i==parameterTypes.length-1){
                        System.out.print(parameterTypes[i].getName()+" args_"+i);
                    }else{
                        System.out.print(parameterTypes[i].getName()+" args_"+i+", ");
                    }

                }

            }
            System.out.print(")");

            //抛出的异常
            System.out.print("\t");
            Class<?>[] exceptionTypes = m.getExceptionTypes();
            if(!(exceptionTypes==null||exceptionTypes.length==0)){
                System.out.print("throws  ");
                for(int i=0;i<exceptionTypes.length;i++){
                    if(i==exceptionTypes.length-1){
                        System.out.print(exceptionTypes[i].getName());
                    }
                    else{
                        System.out.print(exceptionTypes[i].getName()+",");
                    }
                }
            }

            System.out.println();
        }

    }

    //获取构造器
    @Test
    public void ConstructorTest(){

        //getConstructors()方法：获取当前运行时类中声明为public的构造器
        Class<Persons> clazz = Persons.class;
        Constructor<?>[] constructors = clazz.getConstructors();

        for(Constructor cons:constructors){
            System.out.println(cons);
        }

        System.out.println();

        //getDeclaredConstructors()方法：获取当前运行时类中声明的所有的构造器
        Constructor<?>[] declaredConstructors = clazz.getDeclaredConstructors();
        for(Constructor cons:declaredConstructors){
            System.out.println(cons);
        }


    }
}

//父类
class Creature<T>implements Serializable{
    private char gender;
    public double weight;

    private void breath(){
        System.out.println("生物呼吸");
    }

    public void eat(){
        System.out.println("生物吃东西");
    }
}

//接口
interface MyInterface{
    void info();
}

//子类实现类
class Persons extends Creature<String> implements Comparable<String>,MyInterface{

    private String name;
    public int age;
    public double id;

    public Persons(){

    }

    private Persons(String name){
        this.name=name;
    }

    Persons(String name,int age){
        this.name=name;
        this.age=age;
    }

    private String show(String nation){
        System.out.println("My nation is "+nation);
        return nation;
    }

    public String display(String interest) throws NullPointerException,ClassCastException{
        return interest;
    }


    @Override
    public void info() {
        System.out.println("I am a human");
    }

    @Override
    public int compareTo(String o) {
        return 0;
    }
}
```



```java
public class OtherTest {

    //获取运行时类的父类及其泛型
    @Test
    public void test1(){

        Class<Persons> clazz = Persons.class;
        Type genericSuperclass = clazz.getGenericSuperclass();
        System.out.println(genericSuperclass);

        //获取泛型类型
        ParameterizedType paramType=(ParameterizedType) genericSuperclass;
        Type[] actualTypeArguments = paramType.getActualTypeArguments();
        System.out.println(actualTypeArguments[0].getTypeName());
    }

    //获取运行时类的接口
    @Test
    public void test2(){

        Class<Persons> clazz = Persons.class;
        Class<?>[] interfaces = clazz.getInterfaces();
        for(Class c:interfaces){
            System.out.println(c);
        }

        System.out.println();

        //获取运行时类父类实现的接口
        Class<?>[] interfaces2 = clazz.getSuperclass().getInterfaces();
        for(Class c:interfaces2){
            System.out.println(c);
        }
    }
}
```



```java
/**
 * @author lycprimer
 * @create 2021-01-15 16:55
 *
 * 调用运行时类中指定的结构：属性、方法、构造器
 */
public class SpecifiedTest {

    /**
     * 不理想，了解即可
     * @throws Exception
     */
    @Test
    public void specifiedField() throws Exception {

        Class<Persons> clazz = Persons.class;

        //创建运行时类的对象
        Persons p=clazz.newInstance();

        //获取指定的属性:要求运行时类中的属性声明为public
        //通常不采用此方法
        Field id = clazz.getField("age");

        //设置当前属性的值
        //set()方法：参数1：指明设置哪个对象的属性  参数2：属性值
        id.set(p,1001);

        //获取当前属性的值
        //get()方法：参数：获取哪个对象的当前属性值
        int pId =(int) id.get(p);
        System.out.println(pId);
    }

    /**
     *如何获取、操作运行时类指定的属性----需要掌握
     */
    @Test
    public void specifiedField2() throws Exception {

        Class<Persons> clazz = Persons.class;

        Persons p = clazz.newInstance();

        //getDeclaredField(String fieldName)：获取运行时类中指定变量名的属性
        Field name = clazz.getDeclaredField("name");

        //保证当前属性是可访问的，而不是只能获取不能访问
        name.setAccessible(true);

        name.set(p,"Tom");

        System.out.println(name.get(p));
    }


    /**
     *如何获取、操作运行时类指定的方法----需要掌握
     */
    @Test
    public void specifiedMethod() throws Exception {

        Class<Persons> clazz = Persons.class;

        Persons p = clazz.newInstance();

        //获取指定的某个方法
        //getDeclaredMethod()方法：参数1：指明获取的方法的名称  参数2：指明获取的方法的形参列表(可变形参)
        Method show = clazz.getDeclaredMethod("show", String.class);

        //保证当前方法是可访问的
        show.setAccessible(true);

        //invoke()方法：参数1：方法的调用者   参数2：给方法形参复制的实参
        //invoke方法的返回值即为对应类中调用的方法的返回值
        Object returnValue = show.invoke(p, "China");
        System.out.println(returnValue);

        System.out.println("*************如何调用静态方法****************");

        Method showDesc = clazz.getDeclaredMethod("showDesc");
        showDesc.setAccessible(true);

        Object invoke = showDesc.invoke(Person.class);
        System.out.println(invoke);
    }

    /**
     *如何获取、操作运行时类指定的构造器----需要掌握
     */
    @Test
    public void specifiedConstructor() throws Exception {

        Class<Person> clazz = Person.class;

        //获取指定构造器
        //getDeclaredConstructor()方法：参数：指明构造器的参数列表
        Constructor<Person> declaredConstructor = clazz.getDeclaredConstructor(String.class);

        //保证此构造器是可访问的
        declaredConstructor.setAccessible(true);

        //调用此构造器创建运行时类的对象
        Person per = declaredConstructor.newInstance("Tom");
        System.out.println(per);

    }
}
```



# ***动态代理***

```java
/**
 * @author lycprimer
 * @create 2021-01-16 9:38
 *
 * 静态代理举例
 * 代理类和被代理类在编译期间就确定下来了
 */
interface ClothFactory{
    void produceCloth();
}

//代理类
class ProxyClothFactory implements ClothFactory{

    private ClothFactory factory;

    public ProxyClothFactory(ClothFactory factory){
        this.factory=factory;
    }

    @Override
    public void produceCloth() {
        System.out.println("代理工厂准备工作...");
        factory.produceCloth();
        System.out.println("代理工厂收尾工作...");
    }
}

//被代理类
class NikeClothFactory implements ClothFactory{

    @Override
    public void produceCloth() {
        System.out.println("Nike工厂生产一批服装");
    }
}


public class StaticProxy {

    public static void main(String[] args) {

        //创建被代理类对象
        NikeClothFactory nike=new NikeClothFactory();

        //创建代理类对象
        ProxyClothFactory proxyClothFactory = new ProxyClothFactory(nike);

        proxyClothFactory.produceCloth();
    }

}
```



```java
/**
 * @author lycprimer
 * @create 2021-01-16 9:51
 *
 * 动态代理举例
 */
interface Human{
    String getBelief();

    void eat(String food);
}

//被代理类
class SuperMan implements Human{

    @Override
    public String getBelief() {
        return new String("I believe I can fly");
    }

    @Override
    public void eat(String food) {
        System.out.println("I like to eat "+food);
    }
}

/**
 * 要想实现动态代理，需要解决的问题：
 * 1.如何根据加载到内存中的被代理类，动态的创建一个代理类及其对象
 * 2.当通过代理类的对象调用方法时，如何动态的调用被代理类中的同名方法
 */
class ProxyFactory{
    //调用此方法，返回一个代理类对象，解决问题1
    public static Object getProxyInstance(Object obj){//obj:被代理类的对象

        MyInvocationHandler handler = new MyInvocationHandler();

        handler.bind(obj);

        return Proxy.newProxyInstance(obj.getClass().getClassLoader(),obj.getClass().getInterfaces(),handler);
    }
}

class MyInvocationHandler implements InvocationHandler{

    private Object obj;//需要使用被代理类的对象进行赋值
    public void bind(Object obj){
        this.obj=obj;
    }

    //当通过代理类的对象调用方法a时，就会自动调用如下方法:invoke()
    //将被代理类要执行的方法a的功能声明再invoke()中
    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {

        //method:即为代理类对象调用的方法，此方法也就作为了被代理类对象要调用的方法
        //obj:被代理类的对象
        Object returnValue = method.invoke(obj, args);
        //上述方法的返回值就作为invoke()方法的返回值
        return returnValue;
    }
}

public class DynamicProxyTest {

    public static void main(String[] args) {

        SuperMan superMan=new SuperMan();
        //proxyInstance：代理类的对象
        Human proxyInstance = (Human) ProxyFactory.getProxyInstance(superMan);

        //当通过代理类对象调用方法时，会自动调用被代理类中同名的方法
        String belief = proxyInstance.getBelief();
        System.out.println(belief);
        proxyInstance.eat("四川麻辣烫");

        System.out.println("*****************************");

        NikeClothFactory nikeClothFactory = new NikeClothFactory();
        ClothFactory proxyFactory = (ClothFactory) ProxyFactory.getProxyInstance(nikeClothFactory);

        proxyFactory.produceCloth();
    }
}
```



# ***Java8新特性***



## 1.Lambda表达式

```java
/**
 * @author lycprimer
 * @create 2021-01-16 11:29
 *
 * Lambda表达式的使用：lambda表达式是对接口的实现，没有接口，也就没有了lambda表达式
 *
 * 1.举例：(o1,o2)->Integer.compare(o1,o2);
 * 2.格式：
 * ->：lambda操作符 或 箭头操作符
 * ->左侧：lambda形参列表(其实是接口中抽象方法的形参列表)
 * ->右侧：lambda体(其实是重写的抽象方法的方法体)
 *
 * 3.lambda表达式的使用(6种情况)
 * 总结：
 *      ->左侧：lambda形参列表的参数类型可以省略(类型推断)，如果lambda形参列表只有一个参数，其小括号()也可省略
 *      ->右侧：lambda体应该使用大括号{}包裹。如果lambda体只有一条执行语句(可能是return语句)，可省略大括号{}和return关键字
 *
 * 4.lambda表达式的本质：作为函数式接口的实例
 *
 * 5.如果一个接口中，只声明了一个抽象方法，则此接口就成为函数式接口
 */
public class LambdaTest2 {

    //语法格式一：无参，无返回值
    @Test
    public void test1() {

        Runnable r1 = new Runnable() {
            @Override
            public void run() {
                System.out.println("I love Beijing TianAn gate");
            }
        };

        r1.run();

        System.out.println("**************************");

        Runnable r2 = () -> System.out.println("I love China");

        r2.run();
    }

    //语法格式二：一个参数，没有返回值
    @Test
    public void test2() {

        Consumer<String> con = new Consumer<String>() {
            @Override
            public void accept(String s) {
                System.out.println(s);
            }
        };

        con.accept("谎言和誓言的区别");

        System.out.println("****************************");

        Consumer<String> con2 = (String s) -> {
            System.out.println(s);
        };

        con2.accept("一个是听的人当真了，一个是说的人当真了");

    }


    //语法格式三：数据类型可以省略，因为其可由编译器推断得出，即“类型推断”
    @Test
    public void test3() {

        Consumer<String> con = (String s) -> {
            System.out.println(s);
        };

        con.accept("一个是听的人当真了，一个是说的人当真了");

        Consumer<String> con2 = (s) -> {
            System.out.println(s);
        };

        con2.accept("一个是听的人当真了，一个是说的人当真了");
    }

    //语法格式四：lambda若只需要一个参数时，参数的小括号可以省略
    @Test
    public void test4() {

        Consumer<String> con2 = (s) -> {
            System.out.println(s);
        };

        con2.accept("一个是听的人当真了，一个是说的人当真了");

        Consumer<String> con3 = s -> {
            System.out.println(s);
        };

        con3.accept("一个是听的人当真了，一个是说的人当真了");
    }

    //语法格式五：lambda需要两个或两个以上的参数，多条执行语句，并且有返回值
    @Test
    public void test5(){

        Comparator<Integer>com1=new Comparator<Integer>() {
            @Override
            public int compare(Integer o1, Integer o2) {
                System.out.println(o1);
                System.out.println(o2);
                return o1.compareTo(o2);
            }
        };

        System.out.println(com1.compare(12, 21));
        System.out.println("********************************");

        Comparator<Integer>com2=(o1,o2)->{
            System.out.println(o1);
            System.out.println(o2);
            return o1.compareTo(o2);
        };

        System.out.println(com2.compare(12, 1));
    }



    //语法格式六：当lambda体只有一条执行语句时，return与大括号若有，均可以省略
    @Test
    public void test6(){

        Comparator<Integer>com1=(o1,o2)->{
          return o1.compareTo(o2);
        };

        System.out.println(com1.compare(12, 6));

        System.out.println("********************************");

        Comparator<Integer>com2=(o1,o2)-> o1.compareTo(o2);

        System.out.println(com2.compare(12, 21));

    }

}
```



```java
/**
 * @author lycprimer
 * @create 2021-01-16 15:38
 *
 * java内置的4大核心函数式接口
 *
 * 消费型接口 Consumer<T>   void accept(T t)
 * 供给型接口Supplier<T>   T get()
 * 函数型接口Function<T,R>   R apply(T t)  注意lambda表达式，先写的是自变量，后写的是函数值，包括BiFunction
 * 断定型接口Predicate<T>   boolean test(T t)
 */
public class LambdaTest3 {

    @Test
    public void test1(){

        happyTime(500, new Consumer<Double>() {
            @Override
            public void accept(Double aDouble) {
                System.out.println("好家伙，我直接好家伙，工资为："+aDouble);
            }
        });

        System.out.println("****************************");

        happyTime(400,money-> System.out.println("薪资为："+money));

    }

    public void happyTime(double money, Consumer<Double> con){
        con.accept(money);
    }

    @Test
    public void test2(){

        List<String>list = Arrays.asList("北京","南京","天津","东京","普京");
        List<String> stringList = filterString(list, new Predicate<String>() {
            @Override
            public boolean test(String s) {
                return s.contains("京");
            }
        });

        System.out.println(stringList);

        System.out.println("*************************");

        List<String> stringList2 = filterString(list, s -> s.contains("京"));

        System.out.println(stringList2);

    }


    //根据给定的规则，过滤字符串，此规则由Predicate接口的方法决定
    public List<String> filterString(List<String>list, Predicate<String>pre){

        ArrayList<String> filterList=new ArrayList<>();
        for(String s:list){
            if(pre.test(s)){
                filterList.add(s);
            }
        }
        return filterList;
    }
}
```



## 2.方法引用

```java
/**
 * @author lycprimer
 * @create 2021-01-16 16:07
 *
 * 方法引用的使用
 *
 * 使用情景：当要传递给lambda体的操作，已经有实现的方法了，可以使用方法引用
 *
 * 方法引用本质上就是Lambda表达式，而Lambda表达式作为函数式接口的实例，所以方法引用也是函数式接口的实例
 *
 * 使用格式：类(对象)::方法名     注意：不需要小括号()
 *
 * 具体分为如下三种情况
 *   对象::非静态方法
 *   类::静态方法
 *   类::非静态方法
 *
 * 方法引用使用的要求：要求接口中的抽象方法的形参列表和返回值类型与方法引用的方法的形参列表和返回值类型相同！
 *                   (针对情况一和情况二)
 *
 */
public class MethodReferenceTest {

    /**
     * 情况一：对象::实例方法
     * Consumer中的void accept(T t)
     * PrintStream中的void println(T t)
     */
    @Test
    public void test1(){

        Consumer<String>con1=str-> System.out.println(str);
        con1.accept("北京");

        System.out.println("*****************");

        PrintStream ps = System.out;
        Consumer<String> con2=ps::println;
        con2.accept("Beijing");
    }


    /**
     * Supplier中的T get()
     * Employee中的String getName()
     */
    @Test
    public void test2(){

        Employee emp=new Employee(1001,"Tom",23,5600);

        Supplier<String> sup1=()->emp.getName();
        System.out.println(sup1.get());

        System.out.println("*****************");

        Supplier<String>sup2=emp::getName;
        System.out.println(sup2.get());
    }

    /**
     *情况二：类::静态方法
     * Comparator中的 int compare(T t1,T t2)
     * Integer中的 int compare(T t1,T t2)
     */
    @Test
    public void test3(){

        Comparator<Integer> com1=(t1,t2)->Integer.compare(t1,t2);
        int result = com1.compare(12, 21);
        System.out.println(result);

        System.out.println("**************************************");

        Comparator<Integer> com2=Integer::compare;
        int result2 = com2.compare(12, 21);
        System.out.println(result2);

    }

    /**
     * Function中的R apply(T t)
     * Math中的Long round(Double d)
     */
    @Test
    public void test4(){

        Function<Double,Long>func1=d->Math.round(d);
        Long apply = func1.apply(3.49);
        System.out.println(apply);

        System.out.println("**************************************");

        Function<Double,Long>func2=Math::round;
        Long apply2= func2.apply(2.45);
        System.out.println(apply2);
    }

    /**
     * 情况三：类::实例方法
     * Comparator中的 int compare(T t1,T t2)
     * String 中的 int t1.compareTo(t2)
     */
    @Test
    public void test5(){

        Comparator<String>com1=(s1,s2)->s1.compareTo(s2);
        System.out.println(com1.compare("abc","abd"));

        System.out.println("******************************************");

        Comparator<String> com2=String::compareTo;
        System.out.println(com2.compare("abd","abm"));

    }

    /**
     * BiPredicate中的 boolean test(T t1,T t2)
     * String中的boolean t1.equals(t2)
     */
    @Test
    public void test6(){

        BiPredicate<String,String>pre1=(s1,s2)->s1.equals(s2);
        System.out.println(pre1.test("abc", "abc"));

        System.out.println("******************************************");

        BiPredicate<String,String>pre2=String::equals;
        System.out.println(pre2.test("abcd", "abcd"));
    }

    /**
     * Function中的R apply(T t)
     * Employee中的String getName()
     */
    @Test
    public void test7(){

        Function<Employee,String>func1=e->e.getName();

        System.out.println(func1.apply(new Employee(1003, "Jerry", 23, 4834)));

        System.out.println("**************************");

        Function<Employee,String>func2=Employee::getName;
        System.out.println(func2.apply(new Employee(1002, "Kitty", 45, 5463)));

    }

}
```



## 3.构造器引用、数组引用

```java
/**
 * @author lycprimer
 * @create 2021-01-17 9:36
 *
 * 构造器引用:
 *      和方法引用类似，函数式接口的抽象方法的形参列表和构造器的形参列表一致
 *      抽象方法的返回值类型积为构造器所属的类的类型
 *
 * 数组引用：
 *      可以将数组看作是一个特殊的类，则写法与构造器一致
 *
 *
 */
public class ConstructorReferenceTest {

    //构造器引用
    //Supplier中的T get()
    @Test
    public void test1(){
        Supplier<Employee>sup=new Supplier<Employee>() {
            @Override
            public Employee get() {
                return new Employee();
            }
        };
        sup.get();
        System.out.println("**********************");

        Supplier<Employee>sup2=()->new Employee();
        sup2.get();
    }

    //Function中的 R apply(T t)
    @Test
    public void test2(){

        Function<Integer,Employee>func1=id->new Employee(id);

        Employee employee=func1.apply(1001);
        System.out.println(employee);

        System.out.println("***********************");

        Function<Integer,Employee>func2=Employee::new;
        Employee employee2=func2.apply(1002);
        System.out.println(employee2);

    }

    //BiFunction中的 R apply(T t,U u)
    @Test
    public void test3(){

        BiFunction<Integer,String,Employee>func1=(id,name)->new Employee(id,name);

        System.out.println(func1.apply(1001, "Tom"));

        System.out.println("***********************");

        BiFunction<Integer,String,Employee>func2=Employee::new;
        System.out.println(func2.apply(1002, "Jerry"));
    }

    /**
     * 数组引用
     * Function中的R apply(T t)
     */
    @Test
    public void test4(){

        Function<Integer,String[]>func1=length->new String[length];
        String[] arr1 = func1.apply(5);

        System.out.println(Arrays.toString(arr1));

        System.out.println("***********************");

        Function<Integer,String[]>func2=String[]::new;
        String[] arr2 = func2.apply(10);
        System.out.println(Arrays.toString(arr2));

    }
}
```



## 4.Stream API



### 1).Stream的实例化

```java
/**
 * @author lycprimer
 * @create 2021-01-17 10:02
 *
 * Stream关注的是对数据的运算，操作CPU
 * 集合关注的是数据的存储，操作内存
 *
 * Stream本身不会存储元素
 * Stream不会改变源对象，相反，会返回一个持有结果的新Stream
 * Stream操作时延迟执行的，意味着它会等到需要结果的时候才执行
 *
 * Stream执行流程：Stream实例化、中间操作、终止操作
 *
 * 说明：
 * 一个中间操作链，对数据源的数据进行处理
 * 一旦执行终止操作，就执行中间操作链，并产生结果。之后不会再被使用
 *
 */
public class StreamAPITest {

    //创建Stream的方式一：通过集合
    @Test
    public void test1(){

        List<Employee> employees = EmployeeData.getEmployees();

        //default Stream<E> stream()方法：返回一个顺序流
        Stream<Employee> stream = employees.stream();

        //default Stream<E> parallelStream()方法：返回一个并行流
        Stream<Employee> parallelStream = employees.parallelStream();

    }

    //创建Stream的方式二：通过数组
    @Test
    public void test2(){

        int[]arr=new int[]{1,2,3,4,5,6};
        //调用Arrays类中的static<T> Stream<T> stream(T[] array)方法:返回一个流
        IntStream stream = Arrays.stream(arr);

        Employee e1=new Employee(1001,"Tom");
        Employee e2=new Employee(1002,"Jerry");

        Employee[]arr2=new Employee[]{e1,e2};

        Stream<Employee> stream2 = Arrays.stream(arr2);
    }

    //创建Stream的方式三：通过Stream的of()
    @Test
    public void test3(){

        Stream<Integer> stream = Stream.of(1, 2, 3, 4, 5, 6);

    }

    //创建Stream的方式四：创建无限流
    @Test
    public void test4(){

        //迭代
        //public static<T> Stream<T> iterate(final T seed,final UnaryOperator<T> f)

        //遍历前是个偶数
        Stream.iterate(0,t->t+2).limit(10).forEach(System.out::println);

        //生成
        //public static<T> Stream<T> generate<Supplier<T> s>
        Stream.generate(Math::random).limit(10).forEach(System.out::println);


    }
}
```



### 2).Stream的中间操作

```java
/**
 * @author lycprimer
 * @create 2021-01-17 10:23
 *
 * Stream的中间操作
 */
public class StreamAPITest2 {

    //筛选与切片
    @Test
    public void test1(){

        List<Employee> list = EmployeeData.getEmployees();
        Stream<Employee> stream = list.stream();

        //filter(Predicate p)---接受Lambda，从流中排除某些元素
        //stream.filter(e->e.getSalary()>4000).forEach(e-> System.out.println(e));  forEach普通写法
        stream.filter(e->e.getSalary()>4000).forEach(System.out::println);

        System.out.println("*************************************");
        //limit(n)---截断流，使其元素不超过给定的数量
        //注意，此时上一个Stream已被关闭，不能再使用，需要生成一个新的
        list.stream().limit(3).forEach(System.out::println);

        System.out.println("*************************************");

        //skip(n)---跳过元素，返回一个跳过的前 n 个元素的流，若流中元素不足 n 个，则返回一个空流
        list.stream().skip(3).forEach(System.out::println);

        System.out.println("************************************");
        //distinct()---筛选，通过流所生成的元素的hashCode()和equals()去除重复元素
        list.add(new Employee(1001,"刘强东",21,8000));
        list.add(new Employee(1001,"刘强东",21,8000));
        list.add(new Employee(1001,"刘强东",21,8000));
        list.add(new Employee(1001,"刘强东",21,8000));

        list.stream().distinct().forEach(System.out::println);

    }


    //映射
    @Test
    public void test2(){

        /**
         * map(Function f)---接收一个函数作为参数，将元素转换为其他形式或提取信息，该函数会被应用到
         *                   每一个元素上，并将其映射成一个新的元素
         */
        List<String>list= Arrays.asList("aa","bb","cc","dd");
        list.stream().map(str->str.toUpperCase()).forEach(System.out::println);

        //获取姓名长度大于3的员工的姓名
        List<Employee>employees=EmployeeData.getEmployees();

        Stream<String> nameStream = employees.stream().map(e -> e.getName());
        nameStream.filter(name->name.length()>3).forEach(System.out::println);

        System.out.println("***********************************************");

        //例：
        //注意:通过方法引用调用方法要写上包名!
        Stream<Stream<Character>> streamStream = list.stream().map(StreamAPITest2::fromStringToStream);
        streamStream.forEach(s->{
            s.forEach(System.out::println);
        });


        System.out.println("**************************************");
        /**
         * flatMap(Function f)---接收一个函数作为参数，将流中的每一个值都换成另一个流
         *                       然后把所有的流连接成一个流
         * 与上面的例子对比可见，flatMap适用于流中嵌套流的情景
         */
        Stream<Character> characterStream = list.stream().flatMap(StreamAPITest2::fromStringToStream);
        characterStream.forEach(System.out::println);

    }

    //将字符串中的多个字符构成的集合转换为对应的Stream的实例
    public static Stream<Character> fromStringToStream(String str){

        ArrayList<Character>list=new ArrayList<>();

        for(Character c:str.toCharArray()){
            list.add(c);
        }

        return  list.stream();
    }


    //排序
    @Test
    public void test3(){

        //sorted()---自然排序
        List<Integer>list=Arrays.asList(12,34,654,23,767,2,-1);
        list.stream().sorted().forEach(System.out::println);

        //抛异常，因为Employee没有实现Comparable接口
//        List<Employee>employees=EmployeeData.getEmployees();
//        employees.stream().sorted().forEach(System.out::println);


        //sort(Comparator com)---定制排序
        List<Employee>employees=EmployeeData.getEmployees();
        employees.stream().sorted((e1,e2)->{
            int ageValue = Integer.compare(e1.getAge(), e2.getAge());
            if(ageValue!=0){
                return ageValue;
            }else{
                return -Double.compare(e1.getSalary(),e2.getSalary());
            }

        }).forEach(System.out::println);
    }

}
```



### 3).Stream的终止操作

```java
/**
 * @author lycprimer
 * @create 2021-01-17 15:14
 *
 * Stream的终止操作:匹配、查找、归约、收集
 */
public class StreamAPITest3 {

    //匹配与查找
    @Test
    public void test1(){

        List<Employee>employees= EmployeeData.getEmployees();

        //allMatch(Predicate p)---检查是否匹配所有元素
        //练习：是否所有员工的年龄都大于18岁
        boolean allMatch = employees.stream().allMatch(e -> e.getAge() > 18);
        System.out.println(allMatch);

        //anyMatch(Predicate p)---检查是否至少匹配一个元素
        boolean anyMatch = employees.stream().anyMatch(e -> e.getSalary() > 10000);
        System.out.println(anyMatch);

        //noneMatch()---检查是否没有匹配的元素
        boolean noneMatch = employees.stream().noneMatch(e -> e.getName().startsWith("雷"));
        System.out.println(noneMatch);

        //findFirst()---返回第一个元素
        Optional<Employee> firstEmployee = employees.stream().findFirst();
        System.out.println(firstEmployee);

        //findAny()---返回当前流中的任意元素
        Optional<Employee> anyEmployee = employees.parallelStream().findAny();
        System.out.println(anyEmployee);

    }

    @Test
    public void test2(){

        List<Employee> employees = EmployeeData.getEmployees();

        //count()---返回流中元素的总个数
        long count = employees.stream().filter(e->e.getSalary()>4000).count();
        System.out.println(count);

        //max(Comparator c)---返回流中最大值
        //练习：返回最高工作
        Stream<Double> salaryStream = employees.stream().map(e -> e.getSalary());
        Optional<Double> maxSalary= salaryStream.max(Double::compare);
        System.out.println(maxSalary);

        //min(Comparator c)---返回流中的最小值
        //练习：返回最低工资的员工
        Optional<Employee> minEmployee = employees.stream().min((e1, e2) -> Double.compare(e1.getSalary(), e2.getSalary()));
        System.out.println(minEmployee);

        //forEach(Consumer c)---内部迭代
        employees.stream().forEach(System.out::println);

    }

    //归约
    @Test
    public void test3(){

        //reduce(T identity, BinaryOperator)---将流中元素反复结合起来，得到一个值，返回T
        //练习：计算1-10的自然数的和
        List<Integer>list= Arrays.asList(1,2,3,4,5,6,7,8,9,10);
        Integer sum = list.stream().reduce(0, Integer::sum);
        System.out.println(sum);

        //reduce(BinaryOperator)---将流中元素反复结合起来，得到一个值，返回Optional<T>
        //练习：计算公司所有员工工资的总和
        List<Employee> employees = EmployeeData.getEmployees();
        Stream<Double> salaryStream = employees.stream().map(e -> e.getSalary());
        //Optional<Double> sumMoney = salaryStream.reduce(Double::sum);
        Optional<Double> sumMoney = salaryStream.reduce((s1,s2)->s1+s2);
        System.out.println(sumMoney);

    }

    //收集
    @Test
    public void test4(){

        //collect(Collector c)---将流转换为其他形式，接收一个Collector接口的实例，用于
        //                       给Stream中元素做汇总
        //练习：查询工资大于4000的员工，结果返回一个List或Set

        List<Employee>employees=EmployeeData.getEmployees();

        Stream<Employee> employeeStream = employees.stream().filter(e -> e.getSalary() > 4000);
        List<Employee> employeeList = employees.stream().filter(e -> e.getSalary() > 4000).collect(Collectors.toList());

        employeeList.forEach(System.out::println);

        System.out.println("***************************************");

        Set<Employee> employeeSet = employees.stream().filter(e -> e.getSalary() > 4000).collect(Collectors.toSet());
        employeeSet.forEach(System.out::println);

    }
}
```



## 5.Optional类

```java
/**
 * @author lycprimer
 * @create 2021-01-17 16:01
 *
 * Optional类：为了避免在程序中出现空指针异常而创建的
 *
 * 常用方法：ofNullable(T t)
 *          orElse(T t)
 *
 */
public class OptionalClassTest {

    @Test
    public void test1(){

        /**
         * Optional.of(T t):创建一个Optional实例，t必须非空
         * Optional.empty()：创建一个空的Optional实例
         * Optional.ofNullable(T t):t可以为null
         */
        Girl girl=new Girl();
        Optional<Girl> optionalGirl = Optional.of(girl);

    }

    @Test
    public void test2(){

        Girl girl=new Girl();
        girl=null;

        Optional<Girl> optionalGirl = Optional.ofNullable(girl);
        System.out.println(optionalGirl);

        //orElse(T t):如果当前的Optional内部封装的x是非空的，则返回内部的x
        //            如果内部的x是空的，则返回orElse()方法中的参数t

        Girl girl1 = optionalGirl.orElse(new Girl("Kitty"));
        System.out.println(girl1);
    }

    @Test
    public void test3(){

        //空指针异常
//        Boy boy=new Boy();
//        String girlName = getGirlName(boy);
//        System.out.println(girlName);

        Boy boy=new Boy();
        boy=null;
        String girlName2 = getGirlName2(boy);
        System.out.println(girlName2);



    }

    public String getGirlName(Boy boy){

        return boy.getGirl().getName();
    }

    //优化getGirlName()方法
    public String getGirlName2(Boy boy){
        if(boy!=null){
            Girl girl=boy.getGirl();
            if(girl!=null){
                return girl.getName();
            }
        }
        return null;
    }

    //使用Optional类的getGirlName()方法
    public String getGirlName3(Boy boy){

        Optional<Boy> boyOptional = Optional.ofNullable(boy);
        Boy boy1 = boyOptional.orElse(new Boy(new Girl("迪丽热巴")));

        Girl girl = boy1.getGirl();

        Optional<Girl> optionalGirl = Optional.ofNullable(girl);
        Girl girl1 = optionalGirl.orElse(new Girl("古力娜扎"));

        return girl1.getName();
    }

    @Test
    public void test4(){

        Boy boy=null;
        boy=new Boy();
        String girlName3 = getGirlName3(boy);
        System.out.println(girlName3);
    }

}
```

