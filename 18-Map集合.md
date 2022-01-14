![image](https://user-images.githubusercontent.com/90488225/149587963-09d497a1-bba4-4bad-8018-631fb7e0b89c.png)  
![image](https://user-images.githubusercontent.com/90488225/149588172-abcc86bf-8cd5-44bb-8f16-0f89222dd8fc.png)  
```java
Map<String, Integer> maps=new HashMap<>();//太经典了
map.put("红星",3);
map.put("Java",1);
map.put("枸杞",100);
map.put("Java",100);//覆盖前面的数据
map.put(null,null);
System.out.println(maps);//{null=null,Java=100,枸杞=100,红星=3}
```
![image](https://user-images.githubusercontent.com/90488225/149589012-5454bb1e-eb74-4fc4-946d-a9a6ed75fa24.png)  
![image](https://user-images.githubusercontent.com/90488225/149589032-e5d28058-b59f-4029-b0a8-16d64e898a6f.png)  
![image](https://user-images.githubusercontent.com/90488225/149589083-595d172a-170f-4445-b9bb-6525a40a88d6.png)  
```java
//添加怨怒是，无序，不重复，无索引
Map<String, Integer>maps=new HashMap<>();
maps.put("iphoneX",10);
maps.put("娃娃",10);
maps.put("iphoneX",100);
maps.put("huawei",100);
maps.put("生活用品",10);
maps.put("手表",10);
//2.清空集合
maps.clear();
//3.判断集合是否为空，为空则返回true，反之false
System.out.println(maps.isEmpty());
//4.根据键值获取对应值:public V get(Object key)
Integer key=maps.get("huawei");
//5.根据键值删除整个元素（删除键会返回键对应的值）
maps.remove("iphoneX");
//6.判断是否包含某个键，包含返回true，反之false
maps.containsKey("iphoneX");
//7.判断是否包含某个值
maps.containsValue(100);
//8.获取全部键的集合 public Set<K> keySet()
Set<String> keys=maps.keySet();//用Set来接，因为键的特点和Set一样，无序，无重复，无索引
//9.获取全部值的集合 Collection<V> values();//如果也用Set来接，重复值会丢
Collection<Integer> values=maps.values();
//10.集合的大小
maps.size();
//11.合并其他map集合
Map<String,Integer> map1=new HashMap<>();
Map<String,Integer> map2=new HashMap<>();
map1.putAll(map2);//把集合map2的元素拷贝一份到map1中去
```
### Map集合的遍历方式
![image](https://user-images.githubusercontent.com/90488225/149592412-2f9f1749-e34c-4043-946d-49012c313093.png)  
```java
Set<String> keys=map.keySet();
for(String key:keys){
    int value=maps.get(key);
}
```
![image](https://user-images.githubusercontent.com/90488225/149592534-335f6053-3595-4c3a-8e66-9e574c7a1af0.png)  
```java
Set<Map.Entry<String,Integer>> entries=maps.entrySet();
for(Map.Entry<String,Integer> entry:entries){
    String key=entry.getKey();
    int value=entry.getValue();
}
```
![image](https://user-images.githubusercontent.com/90488225/149593378-20610a60-aa5f-4577-ac16-0941252ecf66.png)  
```java
maps.forEach((k,v)->{System.out.println(k+"--->"+v);});
```
### 底层原理
![image](https://user-images.githubusercontent.com/90488225/149594183-402e3b98-dee2-4587-aba6-2c133b79267f.png)  
![image](https://user-images.githubusercontent.com/90488225/149594632-1ee21ac2-c88c-4c00-a970-c05f37348fd3.png)  
![image](https://user-images.githubusercontent.com/90488225/149594679-154f1899-7033-4e6d-9c3b-8f3b96e61388.png)  
![image](https://user-images.githubusercontent.com/90488225/149594795-c23f8e45-a1b8-446a-bce3-2b7f1826dc56.png)  
```java
//TreeMap集合自带排序，可排序无重复无索引
Map<Apple, String> maps2=new TreeMap<>(new Comparator<Apple>(){
    @Override
    public int compare(Apple o1,Apple o2){
        return Double.compare(o2.getPrice(),o1.getPrice());
    }
});
```
![image](https://user-images.githubusercontent.com/90488225/149595311-3d3d2e0e-473a-4816-bdcf-220b5bc4f729.png)  


