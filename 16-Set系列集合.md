## Day16
### Set集合特点
无序：存取顺序不一致  
不重复：可以去除重复  
无索引：没有带索引的方法，所以不能使用普通for循环遍历，也不能通过索引来获取元素  

### Set集合实现类特点
HashSet:无序，不重复，无索引  
LinkedHashSet：有序，不重复，无索引  
TreeSet：排序，不重复，无索引  

```java
//看看Set系列集合的特点：HashSet LinkedHashSet TreeSet
HashSet<String> sets=new HashSet<>();//Set<String> sets=new HashSet<>();经典写法
sets.add("MySQL");
```
![image](https://user-images.githubusercontent.com/90488225/149566407-27e5cae0-c286-4787-bc2a-53e512272b3a.png)  
![image](https://user-images.githubusercontent.com/90488225/149566480-71920676-2c6e-44b8-a20c-91a190ff343c.png)  
![image](https://user-images.githubusercontent.com/90488225/149567163-06d4d74b-e11c-4112-ba2a-5ef7f03fc3dd.png)  
![image](https://user-images.githubusercontent.com/90488225/149567369-ae31ce34-ffff-4d24-8760-7902bcf36eb8.png)  
![image](https://user-images.githubusercontent.com/90488225/149568952-42051d7c-d3c4-456e-8db4-0b35f2838ae3.png)  
![image](https://user-images.githubusercontent.com/90488225/149569196-c153c8ed-efff-40d1-af04-905d798fa047.png)  
![image](https://user-images.githubusercontent.com/90488225/149569338-c61b82da-7773-413b-9a84-6f3b96d0d3f9.png)  
![image](https://user-images.githubusercontent.com/90488225/149569807-10c30618-3567-474e-81fd-1d91dff156f8.png)  
Set去重案例，让Set集合吧重复内容（地址可能不同->hashcode会不一样）的对象也去重  
```java
Set<Student> sets=new HashSet<>();

Student s1=new Student("无恙",20,'男');
Student s2=new Student("无恙",20,'男');
Student s3=new Student("周雄",21,'男');

sets.add(s1);
sets.add(s2);
sets.add(s3);
//并不会去重，因为三个对象地址是不一样的，所以哈希值是不一样的，就无法去重，需要重写equals，在idea里面到Student类里面右键选择equals和hashcode即可
```
![image](https://user-images.githubusercontent.com/90488225/149571221-fe58c9c5-8c83-4546-afdd-bc3b959e85a1.png)  
![image](https://user-images.githubusercontent.com/90488225/149571381-eef9622f-5475-46f1-aa50-95d71da063df.png)  
![image](https://user-images.githubusercontent.com/90488225/149571439-f5674bba-a027-42bc-addb-bd7dba84fdd8.png)  
![image](https://user-images.githubusercontent.com/90488225/149571485-510a2569-a752-4aa2-aef8-11fb4c02a4ba.png)  
自定义类型：  
```java
Set<Apple> apples=new TreeSet<>();
apples.add(new Apple("红富士","红色",9.9,500));
apples.add(new Apple("青苹果","绿色",9.9,500));
apples.add(new Apple("绿苹果","青色",9.9,500));
apples.add(new Apple("黄苹果","黄色",9.9,500));
//直接输出会报错的
```
![image](https://user-images.githubusercontent.com/90488225/149571951-a39bcfe7-bcb7-48ec-af36-93ac17f5f6e5.png)  
```java
方法一：
//重写compareTo方法
public int compareTo(Apple o){
    return this.weight-o.weight;//去掉重复的元素
    //return this.weight-o.weight>=0?1:-1;//保留重量重复的元素
}
方法二：
Set<Apple> apples=new TreeSet<>(new Comparator<Apple>(){
    @Override
    public int compare(Apple o1,Apple o2){
        return o1.getWeight()-o2.getWeight();//升序
        //return o2.getWeight()-o1.getWeight();//降序
        //如果是浮点型，建议直接用Double.compare进行比较
        return Double.compare(o2.getPrice(),o1.getPrice());//降序
        return Double.compare(o1.getPrice(),o2.getPrice());//升序
    }
});
apples.add(new Apple("红富士","红色",9.9,500));
apples.add(new Apple("青苹果","绿色",9.9,500));
apples.add(new Apple("绿苹果","青色",9.9,500));
apples.add(new Apple("黄苹果","黄色",9.9,500));

//简化Tips:
Set<Apple> apples=new TreeSet<>(new Comparator<Apple>(){
    @Override
    public int compare(Apple o1,Apple o2){
        return Double.compare(o2.getPrice(),o1.getPrice());//降序
    }
});
//可简化为：
Set<Apple> apples=new TreeSet<>((o1,o2)->Double.compare(o2.getPrice(),o1.getPrice()) );
```
![image](https://user-images.githubusercontent.com/90488225/149573006-91aa77cb-182f-451d-827b-6a83a5f9782f.png)  
![image](https://user-images.githubusercontent.com/90488225/149573581-f69bf5a9-7ccc-47ce-9b0e-76ac91df4a56.png)  
总结：  
![image](https://user-images.githubusercontent.com/90488225/149574223-936354b6-390e-417d-9a8c-3f722e5119d1.png)  

