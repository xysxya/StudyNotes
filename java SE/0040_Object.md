# Object

Object 是所有类的父类

## Object 是所有类的父类

声明一个类的时候，是默认继承了 Object 类的。

## toString()

Object 类是默认提供 toSting() 方法，所以所有的类都有 roString() 方法。

toString() 方法是返回当前对象的**字符串表达**

## finalze()

当一个对象没有任何引用指向时，他就满足垃圾回收的条件。

当它被垃圾回收的时候，finalize() 就会被调用。

finalize() 方法是由虚拟机 jvm 调用的，并非是开发人员调用。

# equals()

equals() 方法用于判断两个对象是否相同。

## ==

这不是 Object 中的方法，但是也能用于判断两个对象是否相同。

更准确的讲，用于判断两个引用，是否指向了同一个对象。

## hashCode()

hashCode() 返回对象的一个哈希值。