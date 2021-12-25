## day3
### 多态
同类型的对象，执行同一个行为，会表现出不同的行为特征  
常见类型：
父类类型 对象名称=new 子类构造器;
接口 对象名称=new 实现类构造器;

#### 多态访问特点
方法调用：编译看左边，运行看右边  
变量调用：编译看左边，运行也看左边(多态侧重行为多态）

#### 多态的前提
有继承/实现关系；有父类引用指向子类对象；有方法重写  

#### 多态的优势
在多态形式下，右边对象可以实现解耦合，便于扩展和维护
```java
Animal a=new Dog();
a.run();//如果需要，可以直接把Dog()换成Cat(),后续业务行为随对象而改变，后续代码无需修改
```
定义方法的时候，使用父类型作为参数，该方法就可以接收着父类的一切子类对象，体现出多态的扩展性和便利  

#### 多态的问题
多态下不能使用子类的独有功能  
为了解决，我们可以引入强制类型转换的概念  
自动类型转换：（从子到父）子类对象赋值给父类类型的变量指向  
强制类型转换：（从父到子）子类 对象变量=（子类）父类类型的变量  
作用：可以解决多态下的劣势，实现调用子类独有的功能  
```java
Animal a2=new Tortoise();
a2.run();
Tortoise t=(Tortoise) a2;
t.layEggs();
```
注意：如果强制类型转换后的类型和对象真实类型不是同一种类型，那么在转换的时候就会出现ClassCastException
```java
Animal t=new Tortoise();
Dog d=(Dog) t;//出现异常ClassCastException
```
#### instanceof
Java建议强制类型转换前使用instanceof判断当前对象的真实类型，再进行强制类型转换  
用法：变量名 instanceof 真实类型  
判断关键字左边的变量指向的对象的真实类型，是否是右边的类型或是其子类类型，是则返回true，反之，返回false  
```java
Animal a2=new Tortoise();
a2.run();

if(a2 instanceof Tortoise){
    Tortoise t=(Tortoise) a2;
    t.layEggs();
}else if(a2 instanceof Dog){
    Dog d=new Dog();
    d.lookDoor();
}
```
ps: 在开发中，以下情况要考虑用instanceof保证安全  
```java
public static void go(Animal a){}
```
此处传入的参数既可以是Tortoise也可以是Dog，无法预测，所以在该函数内操作时尽量多用instanceof验证  

#### 总结
强制类型转换可以转换成真正的子类类型，从而调用子类独有的功能  
有继承关系/实现的2两个类型就可以进行强制转换，编译无问题  

### 内部类
内部类就是定义在一个类里面的类，里面的类可以理解为（寄生），外部类可以理解为（宿主）  

当一个事物的内部，还有一个部分需要一个完整的结构进行描述，而这个内部的完整结构又只为外部事物提供服务，那么整个内部的完整结构可以使用内部类来设计  
内部类通常可以方便访问外部类的成员，包括私有的成员  
内部类提供了更好的封装性，内部类本身就可以用private protected等修饰，封装性可以做更多控制  

#### 内部类的分类
静态内部类  
```java
public class Outer{
    public static class Inner{
        
    }
}
```
格式：外部类名.内部类名 对象名=new 外部类名.内部类构造器;  
范例：
```java
Outer.Inner in=new Outer.Inner();  
```
当一个类中包含一个完整成分，如汽车类中的发动机类，就可以使用静态内部类  
特点和使用方法和普通类是一样的，类有的成分它都有，只是位置在别人里面而已  
静态内部类可以访问外部类的静态成员，静态内部类不能访问外部类的实例成员，因为外部类的实例成员属于外部类的对象  

成员内部类
局部内部类
匿名内部类

成员内部类
```java
public class Outer{
    public class Inner{
    }
}
```
无static修饰，属于外部类的对象  
格式：外部类名.内部类名 对象名=new 外部类构造器.new内部类构造器();
范例：
```java
Outer.Inner in=new Outer().new Inner();
```
无static修饰，属于外部的对象  
可以直接访问外部类的静态成员，实例方法中可以直接访问外部类的实例成员  
在成员内部类中访问所在外部类对象的格式：外部类名.this  

局部内部类（了解即可）无意义  

### 匿名内部类
本质上是一个没有名字的局部内部类，定义在方法中，代码块中等  
作用：方便创建子类对象，最终目的为了简化代码编写  
格式：  
new 类|抽象类名|接口名(){
    重写方法;
}
```java
Employee a=new Employee(){
    public void work(){
    }
};
a.work();
```
匿名内部类是没有名字的内部类  
匿名内部类写出来就会产生一个匿名内部类的对象  
匿名内部类的对象类型相当于是当前new的那个类型的子类类型  

#### 匿名内部类的常见使用语法
```java
//游泳接口
public interface Swimming{
    void swim();
}
//测试类
public class JumppingDemo{
    public static void main(String[] args){
        Swimming s1=new Swimming(){
            @override
            public void swim(){
                System.out.prinln("the teacher swim faster");
            }
        };
        go(s1);
    }
    //定义一个方法让角色一起来比赛
    public static void goSwimming(Swimming swimming){
        swimming.swim();
    }
}
```
#### 总结
开发中不是我们要去主动定义匿名内部类的，而是别人需要我们写或者我们可以写的时候才会使用，匿名内部类的代码可以实现代码的进一步简化（回归主题）  





