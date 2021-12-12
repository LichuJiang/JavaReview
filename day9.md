## day9
### Arrays类
```java
int[] arr={1,2,3,4,5};
System.out.println(Arrays.toString(arr));//转为string内容
Arrays.sort(arr);//升序排序
int index = Arrays.binarySearch(arr,4);//二分搜索技术，如果找到了就返回下标，如果没找到就返回负数，而且负数的绝对值是按照升序排序时，元素应该插入数组的位置的下标
//注意：binarySearch需要对已经排序的数组使用，未排序可能找不到元素
```
#### 自定义数组排序规则，Comparator比较器对象
```java
//Arrays的sort方法对于有值特性的数组是默认升序排序
//自定义比较器对象，只能支持引用类型的排序！！
int[]ages1={3,1,4,2};
Arrays.sort(ages1,new Comparator<>());
