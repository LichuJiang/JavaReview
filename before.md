## Static 静态
方法：
1.实例方法：无static修饰的，属于对象的
2.静态方法：有static修饰，属于类和对象共享的

调用方法：
1.类名.静态成员方法同一个类中访问静态成员类名可以不写
2.对象.实例成员方法
3.对象.静态成员方法（不推荐，因为会比类直接访问更慢）

Static应用：
### 工具类：对此需要用到的功能，可以将这些功能封装成静态方法放在一个类中变成工具类。
工具类中，需要将工具类构造器私有，这样就不让工具类对外产生对象，直接通过类名访问即可，可以优化内存。
```java
public class VerifyTool{
    private VerityTool(){}
    public static String createCode(int n){}
}
```
工具类中的方法不要用实例方法做，因为实例方法需要创建对象，此时调用对象只是为了调用方法，这样只会浪费内存。

## 代码块：
### 静态代码块：
在类中和类一起生成，自动执行一次，比main还先，可以用来进行一些静态数据的初始化static{}
### 实例代码块：
{}
属于对象的，与对象一起加载，自动触发执行，优先于构造器
初始化块：
```java
{
   id=nextId;
   nextId++;
}
```
不管使用哪个构造器，都会先初始化id，再运行构造器的主体部分。

## 集合：
### ArrayList:（长度可变）
```java
import java.util.ArrayList;  
ArrayList<T> array=new ArrayList<>();  
boolean add(E e); 将指定元素加到末尾  
void add(int index, E element);在集合中指定位置添加元素  
boolean remove(object);删除指定元素  
E remove(int index);删除指定位置的怨怒是，返回被修改的元素  
E set(int index, E element);修改指定位置的元素，返回被修改的元素  
E get(int index); 获取指定元素  
int size(); 返回集合中元素的个数  
```
### String:
```java
String()创建空白字符串对象，无内容   
String(String original)根据传入字符串创建字符串对象  
String(char[] chs)根据字符数组内容创建字符串对象  
String(byte[] chs)根据字节数组的内容创建字符串对象  
boolean equals(Object obj)  
char charAt(int index)返回索引处char的值  
int length()返回此字符串的长度  
toCharArray()转成字符串数组  
eg:  
char[] chars=name.toCharArray();
for(int i=0;i<chars.length();i++){  
    char ch=char[i];
    System.out.println(ch);
}
String substring（int beginIndex, int endIndex) 截取内容：包前不包后
String substring(int beginIndex) 从当前索引一直截取到末尾
String replace(CharSequence target, CharSequence replacement)
eg:
String name3="金三胖是最厉害的80后"
String rs3=name3.replace("金三胖","***");
***是最厉害的80后

boolean contains(CharSequence s)
boolean startsWith(String prefix)
String[] split(String s)
eg:
String name4="wbq,jnl,cyf";
String[] names=name4.split(",");
for(int i=0;i<names.length;i++){
    System.out.println("select: "+names[i]);
}
```

### 随机数
```java
import java.util.Random;

Random r=new Random();
int index=r.nextInt(data.length());
char c=data.charAt(index);
```
