## day3
### 多态
同类型的对象，执行同一个行为，会表现出不同的行为特征  
常见类型：
父类类型 对象名称=new 子类构造器;
接口 对象名称=new 实现类构造器;

#### 多态访问特点
方法调用：编译看左边，运行看右边  
变量调用：编译看左边，运行也看左边(多态侧重行为多态）

#### 多态的前提
有继承/实现关系；有父类引用指向子类对象；有方法重写  

#### 多态的优势
在多态形式下，右边对象可以实现解耦合，便于扩展和维护
```java
Animal a=new Dog();
a.run();//如果需要，可以直接把Dog()换成Cat(),后续业务行为随对象而改变，后续代码无需修改
```
定义方法的时候，使用父类型作为参数，该方法就可以接收着父类的一切子类对象，体现出多态的扩展性和便利  

#### 多态的问题
多态下不能使用子类的独有功能  
为了解决，我们可以引入强制类型转换的概念  
自动类型转换：（从子到父）子类对象赋值给父类类型的变量指向  
强制类型转换：（从父到子）子类 对象变量=（子类）父类类型的变量  
作用：可以解决多态下的劣势，实现调用子类独有的功能  
```java
Animal a2=new Tortoise();
a2.run();
Tortoise t=(Tortoise) a2;
t.layEggs();
```
注意：如果强制类型转换后的类型和对象真实类型不是同一种类型，那么在转换的时候就会出现ClassCastException
```java
Animal t=new Tortoise();
Dog d=(Dog) t;//出现异常ClassCastException
```
#### instanceof
Java建议强制类型转换前使用instanceof判断当前对象的真实类型，再进行强制类型转换  
用法：变量名 instanceof 真实类型  
判断关键字左边的变量指向的对象的真实类型，是否是右边的类型或是其子类类型，是则返回true，反之，返回false  
```java
Animal a2=new Tortoise();
a2.run();

if(a2 instanceof Tortoise){
    Tortoise t=(Tortoise) a2;
    t.layEggs();
}else if(a2 instanceof Dog){
    Dog d=new Dog();
    d.lookDoor();
}
```
ps: 在开发中，以下情况要考虑用instanceof保证安全  
```java
public static void go(Animal a){}
```
此处传入的参数既可以是Tortoise也可以是Dog，无法预测，所以在该函数内操作时尽量多用instanceof验证  

#### 总结
强制类型转换可以转换成真正的子类类型，从而调用子类独有的功能  
有继承关系/实现的2两个类型就可以进行强制转换，编译无问题  

