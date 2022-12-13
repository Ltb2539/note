# 基础

## 函数

### 定义函数

fun定义方法，方法名sum，传参a和b都是Int类型，返回值为Int

```java
public int sum(int a,int b){
    return a+b
}
```

```kotlin
fun sum (a:Int,b:Int):Int{
	return a+b
}
```

### 默认值

允许定义方法时赋予默认值，当没有赋值时使用默认值

在java，只能用多态实现

```java
sun(1)

public int sum(int a,int b){
    return a+b
}
public int sum(int a){
    return a+2
}
```

```kotlin
sum(1)

fun sum (a:Int,b:Int = 2):Int{
	return a+b
}
```

### 指定传参

```java
sum(1,2,3,4)

public int sum(int a,int b,int c,int d){
    return a+b/c*d
}
```

```kotlin
sum(d=4,a=1,c=3,b=2)

fun sum(a:Int,b:Int,c:int,d:Int){
	return a+b/c*d
}
```

### 返回值

**Unit类型**,没有返回值类型默认返回unit

```java
public void sum(){
   
}
```

```
fun sum():Unit{

}
```

### 异常

TODO

```

```



## 变量定义

### var 变量

```java
String str = "123"
```

```kotlin
var str:String = "123"
```

### val 私有常量

带有get方法,通过方法获取

```java
private final static String str = "123"
public void getStr(){
     return str
}
```

```kotlin
val str:String = "123"
```

### const val 公有常量

直接获取

```java
public final static String str = "123"
```

```kotlin
const  val str:String = "123"
```

## 数据类型

同Java

## 常用语句

### range

```java
int a = 2;
if( a=>0 && a<=3 ){}
```

```kotlin
var a = 1
if( a in 0..3){}
```

### when

允许返回值,

```java
int a = 2;
switch(a){
	case 1:
		break;
	case 2:
		break;
    default:
}
```

```kotlin
var a = 2
var b = when(a){
	1 -> a+1
	2 -> a+2
    else -> {
              	a
            }
}
```

### 拼接字符串

```java
String str = "1+2 = " + (1+2);			//1+2 = 3
```

```kotlin
var a = 1
var b = 2
var str = "$a+$b = ${a+b}"				//1+2 = 3
```

