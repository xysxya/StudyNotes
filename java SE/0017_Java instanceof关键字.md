# instanceof

严格来说 instanceof 是 Java 中的一个双目运算符，由于它是由字母组成的，所以也是 Java 的保留关键字。

在 Java 中可以使用 instanceof 关键字判断一个对象是否为一个类（或接口、抽象类、父类）的实例

语法格式如下所示。

```
boolean result = obj instanceof ClassName
```


下面介绍 Java instanceof 关键字的几种用法。

1.声明一个 class 类的对象，判断 obj 是否为 class 类的实例对象（很普遍的一种用法），如以下代码：

```
Integer integer = new Integer(1);
System.out.println(integer instanceof  Integer);    // true
```

2.声明一个 class 接口实现类的对象 obj，判断 obj 是否为 class 接口实现类的实例对象，如以下代码：

Java 集合中的 List 接口有个典型实现类 ArrayList。

```
public class ArrayList<E> extends AbstractList<E>
        implements List<E>, RandomAccess, Cloneable, java.io.Serializable
```

所以我们可以用 instanceof 运算符判断 ArrayList 类的对象是否属于 List 接口的实例，如果是返回 true，否则返回 false。

```
ArrayList arrayList = new ArrayList();
System.out.println(arrayList instanceof List);    // true
```

或者反过来也是返回 true

```
List list = new ArrayList();
System.out.println(list instanceof ArrayList);    // true
```

3）obj 是 class 类的直接或间接子类
我们新建一个父类 Person.class，代码如下：
public class Person {
}

创建 Person 的子类 Man，代码如下：
public class Man extends Person {
}

测试代码如下：
```
Person p1 = new Person();
Person p2 = new Man();
Man m1 = new Man();
System.out.println(p1 instanceof Man);    // false
System.out.println(p2 instanceof Man);    // true
System.out.println(m1 instanceof Man);    // true
```


第 4 行代码中，Man 是 Person 的子类，Person 不是 Man 的子类，所以返回结果为 false。

值得注意的是 obj 必须为引用类型，不能是基本类型。例如以下代码：

```
int i = 0;
System.out.println(i instanceof Integer);    // 编译不通过
System.out.println(i instanceof Object);    // 编译不通过
```
所以，instanceof 运算符只能用作对象的判断。

当 obj 为 null 时，直接返回 false，因为 null 没有引用任何对象。

```
Integer i = 1;
System.out.println(i instanceof null);    // false
```

所以，obj 的类型必须是引用类型或空类型，否则会编译错误。

当 class 为 null 时，会发生编译错误，错误信息如下：

Syntax error on token "null", invalid ReferenceType

所以 class 只能是类或者接口。

编译器会检查 obj 能否转换成右边的 class 类型，如果不能转换则直接报错，如果不能确定类型，则通过编译。这句话有些难理解，下面我们举例说明。
```
Person p1 = new Person();
System.out.println(p1 instanceof String);    // 编译报错
System.out.println(p1 instanceof List);    // false
System.out.println(p1 instanceof List<?>);    // false
System.out.println(p1 instanceof List<Person>);    // 编译报错
```

上述代码中，Person 的对象 p1 很明显不能转换为 String 对象，那么p1 instanceof String不能通过编译，但p1 

instanceof List却能通过编译，而instanceof List<Person>又不能通过编译了。关于这些问题，可以查看Java语言规

范Java SE8版寻找答案，如图所示。
