## Day10
### lambda表达式
Lambda表达式是JDK8开始后的一种新语法形式  
作用：简化匿名内部类的代码写法  

(匿名内部类被重写方法的形参列表)->{  
    被重写方法的方法体代码  
}  
ps:->是语法形式，无实际含义  

#### Lambda表达式只能简化函数式接口的匿名内部类的写法形式
#### 首先必须是个接口，而且只有一个抽象方法才能简化

原始版本：  
```java
Swimming s1=new Swimming(){
    @Override
    public void swim(){
        System.out.println("teacher swim fast");
    }
};
go(s1);


public static void go(Swimming s)

@FunctionalInterface//一旦加上这个注释，就必须是函数式接口，里面只能有一个抽象方法
interface Swimming{
    void swim();
}
```
简化版本：  
```java
Swimming s1=()->{
    System.out.println("teacher swim fast");
}
go(s1);


public static void go(Swimming s)

@FunctionalInterface//一旦加上这个注释，就必须是函数式接口，里面只能有一个抽象方法
interface Swimming{
    void swim();
}
```
极简版本：  
```java
go(()->{
    System.out.println("teacher swim fast");
});


public static void go(Swimming s)

@FunctionalInterface//一旦加上这个注释，就必须是函数式接口，里面只能有一个抽象方法
interface Swimming{
    void swim();
}
```
