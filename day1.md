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
  public static SingleInstance instance;
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
