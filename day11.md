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


