## day4
### Object
一个类要么默认继承了Object类，要么间接继承了Object类，Object类是Java中的祖宗类  
Object类的方法是一切子类都可以直接使用的  
#### String toString()
默认是返回当前对象在堆内存中的地址信息：类的全限名@内存地址  
父类toString()方法存在的意义就是为了被子类重写，以便返回对象的内容信息，而不是地址信息  

#### public Boolean equals(Object o)
默认是比较当前对象与另一个对象的地址是否相同，相同返回true，不同返回false  
直接比较两个对象的地址是否完全相同可以用“==”代替equals  
父类equals存在的意义就是被子类重写，以便子类自己定制比较规则  

### Objects
Objects和Object类还是继承关系，Objects类是从jdk1.7才开始有的  
Objects的equals方法比较的结果是一样的，但是更安全（会做非空判断）  
```java
String s1=null;
String s2=new String("abc");
System.out.println(s1.equals(s2));//s1是空指针，会报空指针异常
Objects.equals(s1,s2)//不会报错，因为Objects类里面的equals(Object a, Object b)会做非空校验
```
附带Objects.equals方法源码：
```java
public static boolean equals(Object a,Object b){
    return (a==b)||(a!=null&&a.equals(b));
}

