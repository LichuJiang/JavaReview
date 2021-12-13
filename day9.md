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
//参数1
Arrays.sort(ages1,new Comparator<>(){
        public int compare(Integer o1, Integer o2){
            //指定比较规则
            //如果左大于右，返回正整数，如果左小于右，返回负整数，如果左等于右，返回0
            if(o1>o2){
                return 1;
            }else if(o1<o2){
                return -1'
            }
            return 0;
        }
        //另一种简化方案
        return o1-o2;//默认升序
        return -(o1-o2);//默认降序
});
System.out.println(Arrays.toString(ages1);
```
上述是对数值进行排序，还可对对象进行排序：  
```java
Student[] students=new Student[3];
students[0]=new Student(jkl,23,175.5);
students[1]=new Student(uio,18,185.5);
students[2]=new Student(bnm,20,195.5);
System.out.println(Array.toString(students));//打出的是三个地址，如果重写了Student类的toString方法，才可打印内容  

Arrays.sort(students,new Comparator<Student>(){
    @Override
    public int compare(Student 01,Student o2){
        //自己制定比较规则
        return o1.getAge()-o2.getAge();//按照年龄升序排序
        return o2.getAge()-o1.getAge();//按照年龄降序排序
        
        //如果是判断身高，身高为小数
        return Double.compare(o1.getHeight,o2.getHeight);//按照升高升序
        //如果不知道，也可以自己写
        if(o1.getHeight<o2.getHeight) return -1;
        if(o1.getHeight>o2.getHeight) return 1;
    }
});
System.out.println(Arrays.toString(students));
```

