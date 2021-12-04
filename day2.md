## day2
### 枚举
是一种特殊类型，用来做信息的标志和信息的分类  
```java
public enum Season{
  //枚举的第一行必须罗列对象名称
  SPRING,SUMMER,AUTUMN,WINTER;
 }
 public static void move(Season s){
  switch(s){
    case:SPRING:
    case:SUMMER:
    case:AUTUMN:
    case:WINTER:
    }
  }
 ```
 枚举类都是继承了枚举类型：java.lang.Enum  
 枚举都是最终类，不能被继承  
 构造器的构造器都是私有的，枚举不能对外创建对象  
 枚举类的第一行默认都是罗列枚举对象的名称的   
 枚举类相当于是多例模式  
 ### 抽象类  
 修饰符 abstract class 类名{}  
 #### 抽象方法  
 修饰符 abstract 类型 方法名()  
 
 可以被子类继承，充当模板，同时也可以提高代码复用  
 如果父类知道子类要完成某个功能，实现要交给子类时  
 抽象方法只有方法签名，没有方法体，使用abstract修饰  
 如果要继承抽象类，那么这个类必须重写完抽象类的全部抽象方法，否则这个类也必须定义为抽象类  
 
 ### 抽象类注意事项
 有得有失，得到了抽象方法，失去了创建对象的能力  
 抽象类一定有构造器，但是不能创建对象，因为抽象类本身的抽象方法是没有方法体的，是由子类继承后进行具体实现的，抽象本身就意味着不许创建对象，即使抽象类中没有定义抽象方法  
 类有的成员（成员变量，方法，构造器）抽象类都具备  
 抽象类中不一定有抽象方法，但是有抽象方法的类一定是抽象类  
 一个类如果继承了抽象类，必须重写玩抽象类的全部抽象方法，否则这个类必须定义成抽象类  
 abstract不能修饰变量，代码块，构造器，只有抽象类和抽象方法的概念  
 
 ###  final和abstract是什么关系
 互斥关系，因为final修饰的类是不可继承的，而abstract就是想要子类继承从而重写类内的抽象方法  
 抽象方法定义通用功能让子类重写，final定义的方法子类不能重写  
 
 