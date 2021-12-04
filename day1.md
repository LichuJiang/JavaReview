## day1
### 饿汉单例设计模式
定义一个类，构造器私有
定义一个静态变量存储一个对象   
```java
public class SingleInstance{  
  //定义一个公开的静态成员变量存储一个类的对象  
  //加载静态变量的时候就会创建对象了  
  public static SingleInstance instance=new SingleInstance();  
  //把构造器藏起来  
  private SingleInstance(){}  
}  
```
### 懒汉单例设计模式
定义一个类，把构造器私有   
定义一个静态变量存储一个对象  
提供一个返回单例对象的方法 
```java
public class SingleInstance{
  //创建一个静态的成员变量存储本类的对象，注意，此时不初始化对象
  private static SingleInstance instance;
  //私有构造器
  private SingleInstance(){}
  //定义一个方法，让其他地方可以来调用获取一个对象
  public static SingleInstance2 getInstance(){
    if(instance==null){
      instance=new SingleInstance();
      }
      return instance;
    }
}
```
### 继承
子类（派生类），父类（基类，超类）
子类 extends 父类  
子类方法中访问成员（成员变量和成员方法）满足：就近原则  
先子类局部范围找  
然后子类成员范围找  
然后父类成员范围找，还没有就报错  
#### 构造器访问特点
子类中所有构造器默认都会先访问父类中无参构造器，再执行自己  
也可以用super（a,b,c）调用父类有参构造器，用来初始化继承父类数据  
如果父类中没有无参构造器，只有有参构造器，会报错，因为子类是默认调用父类的无参构造器  
所以可以再子类构造器中通过书写super来手动调用父类的有参构造器

### 重写
Override重写注解，写在重写后的方法上，如果重写错了会报错  
重写方法的名称形参列表必须与被重写方法的名称和参数列表一致  
私有方法不能重写  
子类不能重写父类的静态方法，否则会报错（因为静态是大家共享，根本不存在继承） 

### this和super总结
关键字|访问成员变量|访问成员方法|访问构造方法
-|:-:|:-:|:-:|
this| this.成员变量 访问本类成员变量| this.成员方法(...) 访问本类成员方法| this(...) 访问本类构造器
super| super.成员变量 访问父类成员变量| super.成员方法(...) 访问父类成员方法| super(...) 访问父类构造器


### 包
#### 建包
package 拥有者.技术名称
#### 导包
import 包名.类名
相同包下的类可以直接访问，不同包下的类不能直接访问，需要导包
如果两个包内有相同类名，则需如此：
```java
import packagedemo1.cat
xxxxx
//使用默认导包的类，demo1下的cat类
Cat c1=new Cat();
c1.run();

//指定使用demo2下的cat类
packagedemo2.Cat c2=new packagedemo2.Cat();
c2.run();
```
### 权限修饰符
修饰符|同一个类|同一个包中其他类|不同包下的子类|不同包下的无关类
-|:-:|:-:|:-:|:-:
private|y|||
缺省|y|y||
protected|y|y|y|
public|y|y|y|y

tips:  
成员变量一般私有  
方法一般公开  
如果该成员只希望本类访问，使用private修饰  
如果该成员只希望本类，同一个包下的其他类和子类访问，使用protected修饰  

### final
final修饰类，这个类就不能被继承了  
final修饰方法，方法不能被重写  
final修饰变量，变量有且仅能被赋值一次  

final修饰的变量是基本类型，那么变量存储的数据值不能发生改变  
final修饰的变量是引用类型，那么变量存储的地址值不能发生改变，但是地址指向的对象内容是可以发生变化的，例如数组：
```java
final int[] arr={1,2,3};
arr[1]=200;//正确，因为此处final不允许arr的地址改变，但是不影响arr指向的内容的值
```

