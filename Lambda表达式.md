## Day10
### lambda表达式
Lambda表达式是JDK8开始后的一种新语法形式  
作用：简化匿名内部类的代码写法  

(匿名内部类被重写方法的形参列表)->{  
    被重写方法的方法体代码  
}  
ps:->是语法形式，无实际含义  

#### Lambda表达式只能简化函数式接口的匿名内部类的写法形式
#### 首先必须是个接口，而且只有一个抽象方法才能简化

原始版本：  
```java
Swimming s1=new Swimming(){
    @Override
    public void swim(){
        System.out.println("teacher swim fast");
    }
};
go(s1);


public static void go(Swimming s)

@FunctionalInterface//一旦加上这个注释，就必须是函数式接口，里面只能有一个抽象方法
interface Swimming{
    void swim();
}
```
简化版本：  
```java
Swimming s1=()->{
    System.out.println("teacher swim fast");
}
go(s1);


public static void go(Swimming s)

@FunctionalInterface//一旦加上这个注释，就必须是函数式接口，里面只能有一个抽象方法
interface Swimming{
    void swim();
}
```
极简版本：  
```java
go(()->{
    System.out.println("teacher swim fast");
});


public static void go(Swimming s)

@FunctionalInterface//一旦加上这个注释，就必须是函数式接口，里面只能有一个抽象方法
interface Swimming{
    void swim();
}
```
### Lambda表达式简化常见函数式接口
#### 简化Comparator接口的匿名形式
```java
public static void main(String[] args){
    Integer[] ages={6,3,2,5,8};
    Arrays.sort(ages,new Comparator<Integer>(){
        @Override
        public int compare(Integer o1, Integer o2){
            return o2-o1;
        }
    });
    System.out.println("内容："+Arrays.toString(ages));
}
```
简化后：  
```java
public static void main(String[] args){
    Integer[] ages={6,3,2,5,8};
    Arrays.sort(ages,(Integer o1, Integer o2)->{
            return o2-o1;
    });
    System.out.println("内容："+Arrays.toString(ages));
}
```

#### 简化按钮监听器ActionListener的匿名内部类形式
```java
JButtion btn=new JButton("登陆");
//给登陆按钮绑定点击事件监听器
btn.addActionListener(new ActionListener(){
    @Override
    public void actionPerformed(ActionEvent e){
        System.out.println("log in!");
    }
});
```
简化后：  
```java
JButtion btn=new JButton("登陆");
//给登陆按钮绑定点击事件监听器
btn.addActionListener((ActionEvent e)->{
        System.out.println("log in!");
    }
});
```
### Lambda表达式的省略写法(进一步在Lambda表达式的基础上继续简化)
1.参数类型可以省略不写  
```java
Arrays.sort(ages,(Integer o1, Integer o2)->{
        return o2-o1;
});
//可简化为
Arrays.sort(ages,(o1,o2)->{
        return o2-o1;
});
```
2.如果只有一个参数，参数类型可以省略，同时()也可以省略  
```java
btn.addActionListener((ActionEvent e)->{
        System.out.println("log in!");
    }
});
//可简化为
btn.addActionListener(e->{
        System.out.println("log in!");
    }
});
```
3.如果Lambda表达式的方法体代码只有一行代码，可以省略大括号不写，同时要省略分号  
```java
btn.addActionListener((ActionEvent e)->{
        System.out.println("log in!");
    }
});
//可简化为
btn.addActionListener(e->System.out.println("log in!"));
```
4.如果Lambda表达式的方法体代码只有一行代码，可以省略大括号不写。此时如果这行代码是return语句，必须省略return不写，同时也必须省略分号不写  
```java
Arrays.sort(ages,(Integer o1, Integer o2)->{
        return o2-o1;
});
//可简化为
Arrays.sort(ages,(o1,o2)->o2-o1);
```


