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
也可以用super调用父类有参构造器，用来初始化继承父类数据  
如果父类中没有无参构造器，只有有参构造器，会报错，因为子类是默认调用父类的无参构造器  
所以可以再子类构造器中通过书写super来手动调用父类的有参构造器

### 重写
Override重写注解，写在重写后的方法上，如果重写错了会报错  
重写方法的名称形参列表必须与被重写方法的名称和参数列表一致  
私有方法不能重写  
子类不能重写父类的静态方法，否则会报错（因为静态是大家共享，根本不存在继承） 

