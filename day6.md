## day6 & day7
### 包装类
就是8种基本数据类型对应的引用类型  
基本数据类型|引用数据类型
:-:|:-:
byte|Byte
short|Short
int|Integer
long|Long
char|Character
float|Float
double|Double
boolean|Boolean  

为了实现一切皆对象，为8中基本类型提供了对应的引用类型  
后面的集合和泛型其实也只能支持包装类型，不支持基本数据类型 

#### 自动拆箱/装箱
自动装箱：基本数据类型和变量可以直接赋值给包装类型的变量  
自动拆箱：包装类型的变量可以直接赋值给基本数据类型的变量  

#### 包装类的特有功能
包装类的变量默认值可以是null，容错率更高  
```java
Integer age=null;//对
int age=null;//错
```
可以把基本类型的数据转换成字符串类型（用处不大）

调用toString()方法得到字符串结果
也可以直接数字+字符串转为字符串类型  
String rs2=i3+""; 即可  

可以把字符串类型的数值转换成真实的数据类型（很有用)
```java
Integer.parseInt("字符串类型的整数")
Double.parseDouble("字符串类型的小数")

String number="23";
int age=Integer.parseInt(number);
int age=Integer.valueOf(number);

String number1="99.9";
double score=Doubel.parseDouble(number1);
double score=Double.valueOf(number1);
```
注意：对应类型才能转，若字符串类形式上是double，如果要转int会报错  

### 正则表达式
正则表达式可以用一些规定的字符来指定规则，用于校验数据格式的合法性  
eg:
```java
public class RegexDemo{
    public static void main(String[] args){
        //需求：校验qq号码，必须全是数字6-20位
        System.out.println(checkQQ("251425998"));
        
        //正则表达式
        System.out.println(checkQQ2("251425998"));
    }
    public static boolean checkQQ2(String qq){
        return qq!=null&&qq.matches("\\d{6,20}");
    }
    
    
    public static boolean checkQQ(String qq){
        //是否满足要求
        if(qq!=null||qq.length()<6||qq.length()>20){
            return false;
        }
        //判断qq中是否全是数字
        for(int i=0;i<qq.length();i++){
            char ch=qq.charAt(i);
            if(ch<'0'||ch>'9'){
                return false;;
            }
        }
        
        return true;
    }
}
```
### 常用正则表达式
#### 字符类  
正则表达式|含义
:-:|:-:
[abc] | 只能是a,b或c
[^abc] |除了abc以外任何字符
[a-zA-Z]|a到zA到Z，范围两边包括
[a-d[m-p]]|a到d, 或m到p:([a-dm-p]联合)
[a-z&&[def]]|d,e或f(交集)
[a-z&&[^bc]]|a到z,除了b和c:([ad-z]减法)
[a-z&&[^m-p]]|a到z,除了m到p:([a-lq-z]减法)

#### 预定义的字符类（默认匹配一个字符）
正则表达式|含义
:-:|:-:
.|任何字符
\d|一个数字:[0-9]
\D|非数字:[^0-9]
\s|一个空白字符:[\t\n\x0B\f\r]
\S|非空白字符:[^\s]
\w|[a-zA-Z_0-9]英文，数字，下划线
\W|[^w]一个非单词字符

#### 贪婪的两次(配合匹配多个字符)
正则表达式|含义
:-:|:-:
X?|X,一次或根本不
X*|X,零次或多次
X+|X,一次或多次
X{n}|X,正好n次
X{n,}|X,至少n次
X{n,m}|X,至少n但不超过m次

#### 字符串对象提供了匹配正则表达式规则的API
```java
public boolean matches(String regex):判断是否匹配正则表达式，匹配则返回true，不匹配则返回false
```
