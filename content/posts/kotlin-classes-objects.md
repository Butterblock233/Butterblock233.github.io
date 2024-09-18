
+++
title = 'Kotlin类和对象'
date = 2024-09-11T20:29:22+08:00
draft = false
author = 'Butterblock233'
tags = ["Kotlin"]
categories = ["计算机"]
series = ["Kotlin学习日记"]
+++

最近刚好在学习Kotlin这方面的知识，随手记录一下。

## Kotlin的类

Kotlin的类和其他语言基本相同。例如，使用以下代码新建一个名为``Box``的类

```kotlin
class Box{
    val Height:Int
    val Length:Int
    val whitht:Int
    
    fun Volume():Int{
        return	Height*Width*Length
    }
}
```

这段代码描述了一个具有长宽高的类😀

## 类的实例化

在Kotlin中，一个类需要具有构造函数才能够实例化。构造函数定义了一个类在实例化时的行为。

```Kotlin
class Box{
	val Height:Int
	val Length:Int
	val Width:Int

	fun Volume():Int{
		return	Height*Width*Length
	}
    //一个构造器
	constructor(H:Int, L:Int, W:Int){
		this.Height = H
		this.Width = W
		this.Length = L
	}
}
```

有了这个构造器后，我们就可以实例化这个类了。

```kotlin
fun main(){
    //实例化Box类：
	val myBox:Box=Box(3,2,3)
	println(myBox.Volume())
}
//运行结果：18
```

## 进一步优化

回顾一下刚刚的构造函数代码：

```Kotlin
	constructor(H:Int, L:Int, W:Int){
		this.Height = H
		this.Width = W
		this.Length = L
	}
```

是不是感觉又臭又长？事实上，Kotlin允许了一种更加简便的方法🤔：

```Kotlin
class Box(H: Int, L: Int, W: Int) {
	val Height:Int = H
	val Length:Int = L
	val Width:Int = W

	fun Volume():Int{
		return	Height*Width*Length
	}
}
```

这样一来代码有所简化，~~也就少了两个大括号~~。但作为偷懒到极致的程序员，这个程度显然是不够的😃。Kotlin对此提供了一个更简洁的语法糖：

```Kotlin
class Box(val Height: Int, val Width: Int,val Length:Int) {
	fun Volume():Int{
		return	Height*Width*Length
	}
}
```

这样，变量的声明、类的构造、参数的传递一步到位，代码简洁多了🤗。除此之外，这样的声明还允许指定默认值：

```Kotlin
class Box(val Height: Int, val Width: Int,val Length:Int=1) {/**/}
```



## 主构造函数和从构造函数

在刚刚的代码中，我们把构造函数直接放到了类名后面，用一个小括号包裹。这种构造方法被称为**主构造函数**（ *primary constructor*），而在``body``中（很抱歉想不到合适的中文翻译）的``construtor``代码片段，则被成为**从构造函数**（*secondary constructors*）。不同于次构造函数，主构造函数块不会包含可执行的代码。如果想在类初始化的同时执行代码，可以使用``init{}``代码片段，例如：

```Kotlin
class Box(val Height: Int, val Width: Int,val Length:Int) {
	fun Volume():Int{
		return	Height*Width*Length
	}
    init{
        println("初始化成功")
    }
}
```

