# Java ArrayList

ArrayList 类位于 java.util 包中，使用前需要引入它，语法格式如下：
```
import java.util.ArrayList; // 引入 ArrayList 类

ArrayList<E> objectName =new ArrayList<>();　 // 初始化
```

ArrayList 是一个数组队列，提供了相关的添加、删除、修改、遍历等功能。<E> 只能是引用数据类型,这是我们就需要基本数据类型的**包装类**。

|基本类型      |引用类型      |
|:--------:|:--------:|
|boolean|Boolean|
|byte|Byte|
|short|Short|
|int|Integer|
|long|Long|
|float|Float|
|double|Double|
|char|Character|

## 添加与访问元素

ArrayList 类提供了很多有用的方法，添加元素到 ArrayList 可以使用 add() 方法，而访问元素可以使用get方法:

```
import java.util.ArrayList;

public class Test {

	public static void main(String[] args) {
		ArrayList<String> sites=new ArrayList<String>();
		sites.add("Google");
		sites.add("yang");
		sites.add("hao");
		System.out.println(sites.get(1));
        System.out.println(sites);


	}

}

```

运行结果
~~~
yang
[Google, yang, hao]
~~~

## 修改元素

如果想要修改ArrayList中的元素可以使set()方法
```
import java.util.ArrayList;

public class Test {

	public static void main(String[] args) {
		ArrayList<String> sites=new ArrayList<String>();
		sites.add("Google");
		sites.add("yang");
		sites.add("hao");
		System.out.println(sites);
		sites.set(1,"Yang");//第一个参数为索引位置，第二个为要修改的参数
		sites.set(2,"Hao");
		System.out.println(sites);
	}

}
```
运行结果
```
[Google, yang, hao]
[Google, Yang, Hao]
```

## 删除元素

删除元素我们使用remove（）方法

```
import java.util.ArrayList;

public class Test {

	public static void main(String[] args) {
		ArrayList<String> sites=new ArrayList<String>();
		sites.add("Hello");
		sites.add("yang");
		sites.add("hao");
		sites.add("NB")
		System.out.println(sites);
		sites.remove(3);
		System.out.println(sites);
	}

}
```
运行结果
```
[Hello, yang, hao, NB]
[Hello, yang, hao]
```

## 计算大小

计算ArrayList的大小我们使用size()

```
import java.util.ArrayList;

public class Test {

	public static void main(String[] args) {
		ArrayList<String> sites=new ArrayList<String>();
		sites.add("Hello");
		sites.add("yang");
		sites.add("hao");
		sites.add("NB");
		System.out.println(sites.size());
		sites.remove(3);
		System.out.println(sites.size());
	}

}
```

运行结果
```
3
4
```

## 遍历ArrayList

在我们有了size（），就可以用来遍历数组；
```
import java.util.ArrayList;

public class Test {

	public static void main(String[] args) {
		ArrayList<String> sites=new ArrayList<String>();
		sites.add("Hello");
		sites.add("yang");
		sites.add("hao");
		sites.add("NB");
		for(int i=0;i<sites.size();i++) {
			System.out.println(sites.get(i));
		}
	}

}
```

运行结果
~~~
Hello
yang
hao
NB
~~~

ArrayList 排序
Collections类是一个非常有用的类，位于,java.util包中，提供的sort()方法可以对字符或者数字列表进行排序
```
import java.util.ArrayList;
import java.util.Collections;

public class Test {

	public static void main(String[] args) {
		ArrayList<String> sites=new ArrayList<String>();
		sites.add("Hello");
		sites.add("yang");
		sites.add("hao");
		sites.add("NB");
		sites.add("apple");
		Collections.sort(sites);
		for(String i:sites) {
			System.out.println(i);
		}
		
	}

}
```

