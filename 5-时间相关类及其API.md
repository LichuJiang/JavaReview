## day5
### date类
date类对象在java中代表的是当前所在系统中的时间  
```java
Date d=new Date();//返回日期
public long getTime();//1970年1月1日0点0时0分走到现在的毫秒数  
public Date(long time);//把时间毫秒值转换成Date日期对象
public void setTime(long time);//设置日期对象的时间为当前时间毫秒值对应的时间
eg：计算出当前时间往后走1小时121秒之后的时间是多少
long time2 = System.currentTimeMillis();
time2+=(60*60+121)*1000;
//把时间毫秒值转换成对应的日期对象
Date d2=new Date(time2);
System.out.println(d2);

Date d3=new Date();
d3.setTime(time2);
System.out.println(d3);
```
总结：  
日期对象创建：Date date=new Date();  
获取时间毫秒值： Long time=date.getTime();  
时间毫秒值恢复成日期对象：Date d=new Date(time);或 d.setTime(time);  

### SimpleDateFormat类
可以对Date对象或时间毫秒值格式化成我们喜欢的时间形式  
也可以把字符串的时间形式解析成日期对象  

格式化：  
Date对象->2099年11月11日 11：11：  
时间毫秒值->2099年11月11日 11：11：  

解析：  
2099年11月11日 11：11：11：-> Date对象  

#### SimpleDateFormat的构造器
```java
//1.日期对象
Date d=new Date();
System.out.println(d);

//2.格式化这个日期对象（指定最终格式化的方式）
SimpleDateFormat sdf=new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss EEE a");

//3.开始格式化日期对象沉稳给喜欢的字符串形式
String rs=sdf.format(d);
System.out.println(rs);
//4.格式化时间毫秒值
//请问121秒之后的时间是多少
long time1=System.currentTimeMillis()+121*1000;
String rs2=sdf.format(time1);
System.out.println(rs2);

public Date parse(String source) 从给定字符串的开始解析文本以生成日期
//请计算出2021年8月6日11点11分11秒，往后走2天14小时49分06秒后的时间是多少

//有一个时间2021年08月06日 11：11：11 往后2天14小时49分06秒后的时间是多少
//1.把字符串时间读取
String dateStr = "2021年08月06日 11：11：11"；
//2.吧字符串时间解析成日期对象（重点）：形式必须与被解析时间的形式完全一样否则运行时解析报错
SimpleDateFormat sdf=new SimpleDateFormat("yyyy年MM月dd日 HH:mm：ss");
sdf.parse(dateStr);
//3.往后走2天14小时49分06秒
long time = d.getTime()+(2L*24*60*60+14*60*60+49*60+6)*1000;//加L是为了防止越界
//4.格式化这个时间毫秒值或是结果
System.out.println(sdf.format(time));
```
### SimpleDateFormat格式化
SimpleDateFormat sdf=new SimpleDateFormat("yyyy-MM-dd HH:mm:ss)//必须与被解析时间完全一致  
Date d=sdf.parse(("2021-08-04 11:11:11");  

### Calendar概述
Calendar代表了系统此刻日期对应的日历对象  
Calendar是一个抽象类，不能直接创建对象  
```java
//拿到系统此时日历对象
Calendar cal=Calendar.getInstance();
//获取日历的信息：pulic int get(int field):取日期中某个字段信息
int year=cal.get(Calendar.YEAR);
//public void set(int field, int value):修改日历的某个字段信息
cal.set(Calendar.HOUT,12);
//public void add(int field, int amount):为某个字段增加，减少指定的值
//请问64天后是什么时间
cal.add(Calendar.DAY_OF_YEAR, 64);
//public final Date getTime():拿到此刻日期对象
Date d=cal.getTime();
//public long getTimeInMillis():拿到时间毫秒值
long time=cal.getTimeInMillis();
```
Calendar是可变日期对象，一旦中途改变了，后面全都会不一样了  

### jdk8新日期和时间类
新API严格区分时刻本地日期本地时间，并且运算更方便  
新API几乎全是不变类型，可以放心使用不必担心被修改  
LocalDate，LocalTime，LocalDateTime  
分别表示日期，时间，日期时间对象，他们的类的实例是不可变的对象  
三者构建对象和API都是通用的  
#### 构建方式
```java
public static xxxx now(); 静态方法，根据当前时间创建对象
LocalDate localDate=LocalDate.now();

public static xxxx of(...); 静态方法，指定日期/时间创建对象
LocalDate localDate=LocalDate.of(2009,11,11);
```
#### 修改相关的方法
修改后返回一个新的实例引用，因为上述三个类都是不可变的  
nowTime.plusHours(1);
nowTime.minusHours(1);

#### 其他API
```java
a.equals(b)  
a.isBefore(b)  
a.isAfter(b)  
a.getMonthValue()
a.getDayOfMonth()
```
### instant时间戳
Instant类由一个静态的工厂方法now()可以返回当前时间戳  
```java
Instant instant=Instant.now();
System.out.println("当前时间戳是："+instant.atZone(ZoneId.systemDefault());

Date date=Date.from(instant);//时间戳转日期对象
System.out.println("当前时间戳是："+date);

instant=date.toInstant();//日期转时间戳
System.out.println(instant);
```

### DateTimeFormatter
```java
LocalDateTime ldt=LocalDateTime.now();
DateTimeFormatter dtf=DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss EEE a")
//正向格式化
dtf.format(ldt);
//逆向格式化
ldt.format(dtf);//正逆结果相同

//解析字符串时间
DateTimeFormatter dtf1=DateTimeFormatter.ofPattern("yyyy-MM-dd HH:mm:ss");
//解析当前字符串时间成为本地日期时间对象
LocalDateTime ldt1=LocalDateTime.parse("2019-11-11 11:11:11",dtf1);
```

### Period类
计算日期间隔差异，只能精确到年月日    
```java
LocalDate today=LocalDate.now();

LocalDate birthDate=LocalDate.of(1990,10,13);

Period period=Period.between(birthDate,today);//第二个参数减去第一个参数
System.out.println(period.getYears());//间隔年
System.out.println(period.getMonths());//间隔月
System.out.println(period.getDays());//间隔天
```

### Duration类
计算时间间隔，可以更精确  
```java
LocalDateTime today = LocalDateTime.now();
LocalDateTime birthDate-LocalDateTime.of(1990,10,1,10,50,30); 
System.out.println(birthDate);

Duration duration=Duration.between(birthDate,today);//第二个参数减去第一个参数
System.out.println(duration.toDays());//间隔天数
System.out.println(duration.toHours());//间隔小时数
System.out.println(duration.toMinutes());//间隔分钟数
System.out.println(duration.toMillis());//间隔毫秒数
System.out.println(duration.toNanos());//间隔纳秒数
```
### ChronoUnit类
可以用于在单个时间单位内测量一段时间，这个工具类最全，可用于比较所有时间单位  
