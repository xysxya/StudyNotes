# Arrays类

## 复制数组

数组的长度是不可变的，一旦分配好空间，是多长，就多长，不能增加也不能减少

**for循环复制**

public class HelloWorld {
    public static void main(String[] args) {
        int a [] = new int[]{18,62,68,82,65,9};
         
        int b[] = new int[3];//分配了长度是3的空间，但是没有赋值
         
        //通过数组赋值把，a数组的前3位赋值到b数组
        for (int i = 0; i < b.length; i++) {
            b[i] = a[i];
        }
    }
}

**System.arraycopy方法复制**

把一个数组的值，复制到另一个数组中

 ```
System.arraycopy(src, srcPos, dest, destPos, length)
 ```

src: 源数组
srcPos: 从源数组复制数据的起始位置
dest: 目标数组
destPos: 复制到目标数组的起始位置
length: 复制的长度

```
public class HelloWorld {
    public static void main(String[] args) {
        int a [] = new int[]{18,62,68,82,65,9};
         
        int b[] = new int[3];//分配了长度是3的空间，但是没有赋值
         
        //通过数组赋值把，a数组的前3位赋值到b数组    
        System.arraycopy(a, 0, b, 0, 3);
         
        //把内容打印出来
        for (int i = 0; i < b.length; i++) {
            System.out.print(b[i] + " ");
        }
 
    }
}
```
## 将数组转换成字符串

如果要打印一个数组的内容，就需要通过for循环来挨个遍历，逐一打印

但是Arrays提供了一个toString()方法，直接把一个数组，转换为字符串，这样方便观察数组的内容
```
import java.util.Arrays;
public class temp {

	public static void main(String[] args) {
		int[] a=new int[] {1,2,3,4,5,6};
		String content=Arrays.toString(a);
		System.out.println(content);

	}

}
```
运行结果
```
[1, 2, 3, 4, 5, 6]
```

## 排序

Arrays工具类提供了一个sort方法，只需要一行代码即可完成排序功能。
```
import java.util.Arrays;
public class temp {

	public static void main(String[] args) {
		int[] a=new int[6];
		for(int i=0;i<a.length;i++) {
			a[i]=(int)(Math.random()*100);
		}
		
		String content=Arrays.toString(a);
		System.out.println(content);
		Arrays.sort(a);
		content=Arrays.toString(a);
		System.out.println(content);

	}

}
```
运行结果
```
[1, 33, 71, 37, 66, 95]
[1, 33, 37, 66, 71, 95]
```
## 搜索binarySearch
查询元素出现的位置，注意，在查询前必须先使用sort排序，另外如果数组中有多个相同的元素，那么查询的结果是不准确的,返回的位置是重复元素的第一个位置。
```
import java.util.Arrays;
import java.util.Scanner;
public class temp {

	public static void main(String[] args) {
		int[] a=new int[20];
		int values;
		Scanner input=new Scanner(System.in);
		for(int i=0;i<a.length;i++) {
			a[i]=(int)(Math.random()*100);
		}
		String content=Arrays.toString(a);
		System.out.println(content);
		Arrays.sort(a);
		content=Arrays.toString(a);
		System.out.println(content);
		System.out.println("输入你想要查询的元素：");
		int temp=input.nextInt();
		System.out.println(Arrays.binarySearch(a, temp));

	}

}
```

运行结果
```
[63, 14, 4, 5, 18, 51, 51, 54, 46, 72, 73, 78, 72, 32, 81, 74, 72, 77, 39, 50]
[4, 5, 14, 18, 32, 39, 46, 50, 51, 51, 54, 63, 72, 72, 72, 73, 74, 77, 78, 81]
输入你想要查询的元素：
46
6
```
## 判断是否相同

比较两个数组的内容是否一样,使用equals()方法
```
import java.util.Arrays;
import java.util.Scanner;
public class temp {

	public static void main(String[] args) {
		int[] a=new int[]{1,2,3,4,5};
		int[] b=new int[]{1,2,3,4,3};
		System.out.println(Arrays.equals(a,b));
	}

}
```

运行结果
```
false
```

## 填充
使用同一个值填充整个数组
```
import java.util.Arrays;
public class temp {

	public static void main(String[] args) {
		int[] a=new int[9];
		Arrays.fill(a, 5);
		System.out.println(Arrays.toString(a));
	}

}
```


## 问题

1.首先准备两个数组，他俩的长度是5-10之间的随机数，并使用随机数初始化这两个数组
(向数组填充随机数的办法，参考这里)

然后准备第三个数组，第三个数组的长度是前两个的和
通过System.arraycopy 把前两个数组合并到第三个数组中

```
public class temp {

	public static void main(String[] args) {
		int[] array_1=new int[10];
		int T;
		for(int i=0;i<array_1.length;i++) {
			array_1[i]=(int)(Math.random()*100);
		}
		for(int each:array_1) {
			System.out.print(each+" ");
		}
		System.out.println();
		int[] array_2=new int[10];
		for(int i=0;i<array_2.length;i++) {
			array_2[i]=(int)(Math.random()*100);
		}
		for(int each:array_2) {
			System.out.print(each+" ");
		}
		System.out.println();
		int[] array_3=new int[20];
		System.arraycopy(array_1, 0, array_3, 0, 10);
		System.arraycopy(array_2, 0, array_3, 10, 10);
		for(int each:array_3) {
			System.out.print(each+" ");
		}	
	}

}
```
