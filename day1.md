## day1
### 饿汉单例
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
