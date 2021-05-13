# fianl

fianl 修饰类、方法、基本类型变量和引用的有不同的意思。

# fianl 修饰类

当类被 final 修饰时，表示该不能被继承。

```
public final class Hero{

}

//error
public ADHero extends Hero{

}
```
## fianl 修饰基本类型变量

当基本数据类型被 final 修饰时，表示该变量只有一次赋值的机会。

## final 修饰引用

当 final 修饰引用时，表示该引用只有一次机会指向某个对象。
