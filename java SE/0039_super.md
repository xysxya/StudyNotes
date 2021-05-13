
## 准备一个显式提供无参构造方法的父类

```
//Hero.java
package characotr;

import propetry.Item;

public class Hero {
    public String name;
    protected float hp;

    public void useItem(Item i){
        System.out.println("hero use item");
        i.effect();
    }
    public Hero(){
        System.out.println("Hero 的构造方法");
    }

    public static void main(String[] args) {
        new Hero();
    }

}
```

## 实例化子类，父类的构造方法一定会被调用

实例化一个ADHero(), 其构造方法会被调用

其父类的构造方法也会被调用

并且是父类构造方法先调用

子类构造方法会默认调用父类的 无参的构造方法

```
package characotr;

public class ADHero extends Hero implements AD{

    @Override
    public void physicAttack() {
        System.out.println("进行物理攻击");
    }

    public ADHero(){
        System.out.println("ADHero 的构造方法");
    }

    public static void battleWin(){
        System.out.println("ad Hero battle win");
    }

    public static void main(String[] args) {
        new ADHero();
    }
}
```

运行结果
```
Hero 的构造方法
ADHero 的构造方法
```

## 父类显式提供两个构造方法

```
package characotr;

import propetry.Item;

public class Hero {
    public String name;
    protected float hp;

    public void useItem(Item i){
        System.out.println("hero use item");
        i.effect();
    }
    public Hero(){
        System.out.println("Hero 的构造方法");
    }

    public Hero(String name){
        System.out.println("带有一个参数的构造方法");
    }

    

    public static void main(String[] args) {
        new Hero();
    }

}
```

## 子类显式调用父类带参构造方法

```

package characotr;

public class ADHero extends Hero implements AD{

    @Override
    public void physicAttack() {
        System.out.println("进行物理攻击");
    }

   public ADHero(String name){
        super(name);//显示调用一个参数的构造方法
       System.out.println("ADHero 的构造方法");
   }

    public static void main(String[] args) {
        new ADHero("娜可露露");
    }


}
```

## 调用父类属性
```
//接口
package characotr;

public interface AD {
    public void physicAttack();
}
//子类
package characotr;

public class ADHero extends Hero implements AD {
    int moveSpeed=400;
    @Override
    public void physicAttack() {
        System.out.println("进行物理攻击");
    }

    public int getMoveSpeed(){
        return this.moveSpeed;
    }

    public int getMoveSpeed_2(){
        return super.moveSpeed;//上一个父类
    }
    public static void main(String[] args) {
        ADHero h=new ADHero();
        System.out.println(h.getMoveSpeed());
        System.out.println(h.getMoveSpeed_2());


    }


}
//父类
package characotr;
import propetry.Items;

public class Hero {
    public String name;
    protected float hp;
    int moveSpeed=200;

    public void useItem(Items i){
        System.out.println("hero use item");
        i.effect();
    }
    public Hero(){
        System.out.println("Hero 的构造方法");
    }

    public Hero(String name){
        System.out.println("带有一个参数的构造方法");
    }



    public static void main(String[] args) {
        new Hero();
    }

}
```

## 调用父类方法

```
package characotr;

import propetry.Items;
import propetry.LifePotion;
public class ADHero extends Hero implements AD {
    int moveSpeed=400;
    @Override
    public void physicAttack() {
        System.out.println("进行物理攻击");
    }

    public int getMoveSpeed(){
        return this.moveSpeed;
    }

    public int getMoveSpeed_2(){
        return super.moveSpeed;//上一个父类
    }
    
    publlic void useItem(Items i){
        System.out.println("adhero use item");
        super.useItem(i);
    }
    public static void main(String[] args) {
        ADHero h=new ADHero();
        
        LifePotion h=new LifePotion()；


    }


}
```