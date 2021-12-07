## day4
### Object类
一个类要么默认继承了Object类，要么间接继承了Object类，Object类是Java中的祖宗类  
Object类的方法是一切子类都可以直接使用的  
#### String toString()
默认是返回当前对象在堆内存中的地址信息：类的全限名@内存地址  
父类toString()方法存在的意义就是为了被子类重写，以便返回对象的内容信息，而不是地址信息  

#### public Boolean equals(Object o)
默认是比较当前对象与另一个对象的地址是否相同，相同返回true，不同返回false  
直接比较两个对象的地址是否完全相同可以用“==”代替equals  
父类equals存在的意义就是被子类重写，以便子类自己定制比较规则  

### Objects类
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
```

#### Objects常见方法
public static boolean equals(Object a, Object b)比较两个对象，底层会先进行非空判断，从而可以避免空指针异常，再进行equals比较  
public static boolean isNull(Object obj)判断变量是否为null, 为null返回true，反之返回false  

### StringBuilder类
StringBuilder是一个可变的字符串类，可以看作一个对象容器  
作用：提高字符串的操作效率，如拼接，修改等  

#### StringBuilder构造器
```java  
public StringBuilder()  创建一个空白的可变的字符串对象，不包含任何内容  
public StringBuilder(String str) 创建一个指定字符串内容的可变字符串对象  
public StringBuilder append(任意类型） 添加数据并返回StringBuilder对象本身  
public StringBuilder reverse()  对象内容反转  
public int length()  返回对象内容长度  
public String toString() 通过toString()就可以实现把StringBuilder转换为String  
```
在使用StringBuilder类修改完之后可以转回String类
```java
StringBuilder sb=new StringBuilder();
sb.append("123").append("456");
String st=sb.toString();
```
String拼接效率比StringBuilder效率低  
因为String内容是不可变的，拼接的时候需要创建StringBuilder对象，再从常量池中拿出对象拼接，再转成String对象  
而StringBuilder不需要额外创建其他类对象，可以直接拼接  
定义字符串使用String，如果需要拼接，修改等操作字符串，就使用StringBuilder  

