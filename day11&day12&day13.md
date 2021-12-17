## day11
### 集合的体系结构
### Collection 单列
Collection是个接口，分为List和Set，也都是接口，不可以直接使用的  
List: 添加的元素是有序，可重复，有索引  
eg: ArrayList, LinkedList:有序，可重复，有索引  
Set: 添加的元素是无序，不重复，无索引  
eg: HashSet: 无序，不重复，无索引 LinkedHashSet: 有序，不重复，无索引 TreeSet: 按照大小默认升序排序，不重复，无索引  
```java
//有序，可重复，有索引
Collection list = new ArrayList();
list.add("a");
list.add("a");
list.add(23);
list.add(23);
list.add(false);
list.add(false);
System.out.println(list);//a,a,23,23,false,false

//无序，不重复，无索引
Collection list1 = new HashSet();
list.add("a");
list.add("a");
list.add(23);
list.add(23);
list.add(false);
list.add(false);
System.out.println(list);//a,false,23
```
#### 集合对泛型的支持
集合是支持泛型的，可以在编译阶段约束集合只能操作某种数据类型  
```java
Collection<String> lists=new ArrayList<String>();
Collection<String> lists=new ArrayList<>();//jdk1.7之后泛型类型申明可以省略不写
```
tips:集合和泛型都只能支持引用数据类型，不支持基本数据类型，所以集合中存储的元素都认为是对象  
```java
Collection<int> lists = new ArrayList<>();//错误！
Collection<Integer> lists = new ArrayList<>();//正确！基本数据类型要用包装类/引用数据类型
Collection<Double> lists = new ArrayList<>();//正确！

ps:
Collection<Double> list4=new ArrayList<>();
list4.add(23);///错误！
list4.add(23.0);//正确!
```

### Collection常用API
```java
Collection<String> c=new ArrayList<>();
//1.添加元素
c.add("java");//add方法是boolean类型，所以有返回值
c.add("html");
//2.清空集合元素
c.clear();
//3.判断集合是否为空，空则返回true
c.isEmpty();
//4.获取集合的大小
c.size();
//5.判断集合中是否包含某个元素
c.contains("java");//true
//6.删除某个元素：如果有多个元素默认删除前面的第一个
c.remove("java");//true, 但只删第一个
c.romove("Java");//false
//7.把集合转换成数组
Object[] arrs=c.toArray();//转成Object类可以兼容一切数据类型
System.out.println("数组: "+Arrays.toString(arrs));

Collection<String> c1=new ArrayList<>();
c1.add("java1");
c1.add("java2");
Collection<String> c2=new ArrayList<>();
c2.add("zm");
c2.add("yss");
//addAll 把c2集合中的元素全部倒入到c1中去
c1.addAll(c2);
```
方法名称|说明
:-|:-
public boolean add(E e)|把给定的对象添加到集合中
public void clear()|清空集合中所有的元素
public boolean remove(E e)|把给定的对象在当前集合中删除
public boolean contains(Object obj)|判断当前集合中是否包含给定的对象
public boolean isEmpty()|判断当前集合是否为空
public int size()|返回集合中元素的个数
public Object[] toArray()|把集合中的元素，存储到数组中

### 遍历方式
#### 迭代器
Collection集合获取迭代器：  
```java
Iterator<E> iterator() //返回集合中的迭代器对象，该迭代器对象默认指向当前集合的0索引
```
Iterator中的常用方法：  
```java
boolean hasNext()//询问当前位置是否有元素存在，存在则返回true，不存在则返回false
E next()//获取当前位置的元素，并同时将迭代器对象移向下一个位置，注意防止取出越界
