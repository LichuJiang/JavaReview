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
Collection<String> c=new ArrayList<>();
c.add("a");
c.add("b");
c.add("c");
c.add("d");

//1.得到当前集合的迭代器对象
Iterator<String> it=c.iterator();
String ele=it.next();//ele是 a 
String ele2=it.next();//ele是b

Iterator<String> it=c.iterator();
while(it.hasNext()){
    String ele=it.next();
    System.out.println(ele);
}//输出a,b,c,d
```
迭代器默认位置指向当前集合的索引0，如果越界了会出现NoSuchElementException异常  

#### 增强for循环
既可以遍历集合也可以遍历数组  
是JDK5之后出现的，其内部是一个Iterator迭代器，遍历集合相当于是迭代器的简化写法  
实现了Iterable接口的类才可以使用迭代器和增强for，Collection接口已经实现了Iterable接口  
格式：  
```java
for(元素数据类型 变量名:数组或Collection集合){
    //在此处使用变量即可，该变量就是元素
}


Collection<String> c=new ArrayList<>();
...
for(String ele:c){
    System.out.println(ele);
}
```
增强for循环内是无法改变元素值的，因为增强for只是给了个备份  
#### Lambda表达式遍历集合
jdk8之后开始的Lambda表达式  
Collection结合Lambda遍历的API 
方法名称|说明
:-|:-
default void forEach(Consumer<? super T> action):|结合lambda遍历集合  


```java
Collection<String> c=new ArrayList<>();
c.forEach(new Consumer<String>(){
    @Override
    public void accept(String s){
        System.out.println(s);
    }
}
```
简化后
```java
c.forEach(s->{
    System.out.println(s);
}//c.forEach(s->System.out.println(s));
```
### Collection集合存储自定义类型的对象
```java
Collection<Movie> movies=new ArrayList<>();
movies.add(new Movie("rush hour",9.5,"brandon"));
movies.add(new Movie("ready or not",9.1,"julia"));
movies.add(new Movie("2012",8.5,"jacky"));
System.out.println(movies);//如果类内没有重写toString方法的话，输出的就是地址  
//即使重写了toString方法，可以输出内容了，但集合存入的是地址，操作的还是地址  

for(Movie movie:movies){
    System.out.println("Name: "+movie.getName());
    System.out.println("Score: "+movie.getScore());
    System.out.println("Actor: "+movie.getActor());
}
```
注意：集合中存储的是元素对象的地址！  

### List系列集合
#### List家族独有方法
List集合因为支持索引，所以多了很多索引操作的独特api，其他Collection的功能List也都继承了  
方法名称|说明
:-|:-
void add(int index, E element)|在此集合中的指定位置插入指定的元素
E remove(int index)|删除指定索引处的元素，返回被删除的元素
E set(int index, E element)|修改指定索引处的元素，返回被修改的元素
E get(int index)|返回指定索引处的元素

eg:
```java
ArrayList<String> list=new ArrayList<>();//普通写法
List<String> list=new ArrayList<>();//多态写法
list.add("java");
list.add("java");
list.add("SQL");
list.add("SQL");
//2.在某个索引位置插入元素  
list.add(2,"HTML");
System.out.println(list);//java java html sql sql
//3.根据索引删除元素返回被删除元素
System.out.println(list.remove(2));//html
System.out.println(list);//java java sql sql
//4.根据索引获取元素：public E get(int index) 返回集合中指定位置的元素  
System.out.println(list.get(2));//sql
//5.修改索引位置处的元素: public E set(int index, E element)
//返回修改前的数据
System.out.println(list.set(1,"goslin"));//java
System.out.println(list);//java goslin sql sql
```
ArrayList底层基于数组实现，查询元素快，增删相对慢  
LinkedList底层基于双链表实现，查询元素慢，增删首尾元素快  

#### List集合的遍历方式
1.迭代器  
```java
Iterator<String> it=list.iterator();
while(it.hasNext()){
    String ele=it.next();
    System.out.println(ele);
}
```
2.增强for循环  
```java
for(String ele:lists){
    System.out.println(ele);
}
```
3.Lambda表达式  
```java
lists.forEach(s->{
    System.out.println(s);
});
```
4.for循环(因为List集合存在索引)  
```java
for(int i=0;i<list.size();i++){
    String ele=list.get(i);
    System.out.println(ele);
}
```
#### ArrayList集合底层原理
ArrayList是基于数组实现的：根据索引定位元素快，增删需要做元素的移位操作  
第一次创建集合并添加第一个元素的时候，在底层创建一个默认长度为10的数组  
如果超过10，就扩容到原来的1.5倍再迁移

#### LinkedList集合底层原理
基于双链表实现，查询慢，首尾操作速度很快，所以API大多基于首尾操作  
方法名称|说明
:-|:-
public void addFirst(E e)|在列表开头插入指定元素  
public void addLast(E e)|将指定的元素追加到此列表的末尾
public E getFirst()|返回此列表中的第一个元素
public E getLast()|返回此列表中的最后一个元素
public E removeFirst()|从此列表中删除并返回第一个元素
public E removeLast()|从此列表中删除并返回最后一个元素  
 
#### LinkedList可以完成队列结构和栈结构
```java
//栈
LinkedList<String> stack=new LinkedList<>();
stack.addFirst("1");
stack.addFirst("2");
stack.addFirst("3");
stack.addFirst("4");
System.out.println(stack);//4,3,2,1
System.out.println(stack.getFirst());//4
System.out.println(stack.removeFirst());//4

//队列
LinkedList<String> queue=new LinkedList<>();
queue.addLast("1");
queue.addLast("2");
queue.addLast("3");
queue.addLast("4");
System.out.println(queue.removeFirst());



