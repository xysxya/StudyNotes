# LinkedList

## LInkedList 与 List 接口

与ArrayList一样，LinkedList也实现了List接口，诸如add,remove,contains等等方法。 详细使用，请参考 ArrayList 常用方法，在此不作赘述。

接下来要讲的是LinkedList的一些特别的地方

## 双向链表

除了实现了List接口外，LinkedList还实现了双向链表结构Deque，可以很方便的在头尾插入删除数据

什么是链表结构: 与数组结构相比较，数组结构，就好像是电影院，每个位置都有标示，每个位置之间的间隔都是一样的。 而链表就相当于佛珠，每个珠子，只连接前一个和后一个，不用关心除此之外的其他佛珠在哪里。

```java
package collection;

import java.util.LinkedList;
import charactor.Hero;

public class TestCollection {

    public static void main(String[] args) {
        LinkedList<Hero> doubleList=new LinkedList<Hero>();
        doubleList.addLast(new Hero("hero1"));
        doubleList.addLast(new Hero("hero2"));
        doubleList.addLast(new Hero("hero3"));

        doubleList.addFirst(new Hero("hero4"));
        doubleList.addFirst(new Hero("hero5"));
        doubleList.addFirst(new Hero("hero6"));

        System.out.println(doubleList);

        //在最前面插入新的英雄
        doubleList.addFirst(new Hero("heroX"));
        System.out.println(doubleList);

        //查看最前面的英雄
        System.out.println(doubleList.getFirst());
        //查看最后面的英雄
        System.out.println(doubleList.getLast());

        //查看不会导致英雄被删除
        System.out.println(doubleList);
        //取出最前面的英雄
        System.out.println(doubleList.removeFirst());

        //取出最后面的英雄
        System.out.println(doubleList.removeLast());

        //取出会导致英雄被删除
        System.out.println(doubleList);

    }

}
```
运行结果
```
[hero6, hero5, hero4, hero1, hero2, hero3]
[heroX, hero6, hero5, hero4, hero1, hero2, hero3]
heroX
hero3
[heroX, hero6, hero5, hero4, hero1, hero2, hero3]
heroX
hero3
[hero6, hero5, hero4, hero1, hero2]
```

## 队列-Queue

LinkedList 除了实现了List和Deque外，还实现了Queue接口(队列)。

Queue是先进先出队列 FIFO，常用方法：

- offer 在最后添加元素
- poll 取出第一个元素
- peek 查看第一个元素

```java
package collection;

import java.util.LinkedList;
import java.util.List;
import java.util.Queue;

import charactor.Hero;

public class TestCollection {

    public static void main(String[] args) {
        //和 ArraysList 一样，LinkedList 也实现了 List 接口

        List ll=new LinkedList<Hero>();

        //所不同的是 LinkedList 还实现了 Deque ,进而又实现了 Queue 这个接口
        //Queue 代表了 FIFO 先进先出的队列
        Queue<Hero> q=new LinkedList<Hero>();

        /*
        * 加在队列的最后面
        * 初始化数组
        * */

        q.offer(new Hero("hero1"));
        q.offer(new Hero("hero2"));
        q.offer(new Hero("hero3"));
        q.offer(new Hero("hero3"));

        System.out.println(q);

        Hero h=q.poll();
        System.out.println(h);
        System.out.println(q);

        //把第一个拿出来看一看，但是不取走
        h=q.peek();
        System.out.println("查看第一个元素：\t");
        System.out.println(h);
        System.out.println(q);

    }

}
```
运行结果
```
[hero1, hero2, hero3, hero3]
hero1
[hero2, hero3, hero3]
查看第一个元素：	
hero2
[hero2, hero3, hero3]
```
## ArrayList 和 LinkedList



