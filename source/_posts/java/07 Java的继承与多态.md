---
title: 07 Java的继承与多态
date: 2018-09-09 20:48:50
---
## 继承 
Java继承的实现(只支持单继承,而不是多继承,称为接口的多实现)         
　　　　
多个类中存在相同属性和行为时，将这些内容抽取到单独一个类. 定义类时直接通过extends关键字指明要继承的父类.
子类对象除了可以访问子类中直接定义的成员外,可直接访问父类的所有非私有成员.
　　
### 继承的作用
* 继承提高了代码的复用性。
* 继承的出现让类与类之间产生了关系，提供了多态的前提。
* 不要仅为了获取其他类中某个功能而去继承,  类与类之间要有所属( " is a " )关系)。
　　
### How 如何使用一个继承体系中的功能:　　　　
* 查阅父类功能(定义了共性的功能)　　　　
* 创建子类对象使用功能(因为父类可能不能创建对象, 而且子类提供了更丰富的功能)
* 继承中自子类变量的特点:如果子类出现非私有的同名变量时, 子类访问本类变量用this, 子类访问父类中的同名变量用super.

### 成员变量隐藏
子类成员变量与父类一样，会屏蔽父类中的成员变量，称为“成员变量隐藏”。

### 方法的覆盖（Override）
如果子类方法完全与父类方法相同，即：相同的方法名、相同的参数列表和相同的返回值，只是方法体不同，这称为子类覆盖（Override）父类方法。

在声明方法时最后添加`@Override`注解，`@Override`注解不是方法覆盖必须的，它只是锦上添花，但添加@Override注解有两个好处：
* 提高程序的可读性。
* 编译器检查@Override注解的方法在父类中是否存在，如果不存在则报错。

#### 方法覆盖时应遵循的原则：
> 1. 覆盖后的方法不能比原方法有更严格的访问控制（可以相同）。例如将代码第②行访问控制public修改private，那么会发生编译错误，因为父类原方法是protected。
> 2. 覆盖后的方法不能比原方法产生更多的异常。
> 3. 父类中的私有方法不可以被覆盖。

#### 覆盖的应用：
  + 当子类需要父类的功能，而功能主体子类有自己特有内容时，可以复写父类中的方法，这样也沿袭了父类的功能
  + 构造方法在类继承中的作用          
     构造方法不能继承.由于子类对象要对来自父类的成员进行初始化,因此,在创建子类对象时除了执行子类的构造方法外,还需要调用父类的构造方法.具体遵循如下原则:
    1. 当子类未定义构造方法时,创建对象时将无条件地调用父类的空构造方法,以为每行第一条super(); 
    2. 对于父类的含参数构造方法,子类可以在自己构造方法中使用关键字super来调用它, 但super调用语句必须是子类构造方法中的**第一个**可执行语句； 
    3. 子类在自己定义构造方法中如果没有用super明确调用父类的构造方法，则在创建对象时,将自动先执行父类的无参构造方法,然后再执行自己定义的构造方法。
所以在一个类的设计时如果有构造方法,最好提供一个无参构造方法.因此,系统类库中的类大多提供了无参构造方法,用户编程时最好也要养成此习惯.     
> 【注意】使用this查找匹配的方法时首先在本类查找，找不到时再到其父类和祖先类查找；使用 super 查找匹配方法时，首先到直接父类查找，如果不存在，则继续到其祖先类逐级往高层查找。

## 多态性
体现在父类或者接口的引用指向或者接收自己的子类对象 
作用：多态的存在提高了程序的扩展性和后期可维护性.

发生多态要有三个前提条件：
1. 继承。多态发生一定要子类和父类之间。
2. 覆盖。子类覆盖了父类的方法。
3. 声明的变量类型是父类类型，但实例则指向子类实例。

### 引用类型转换 
并不是所有的引用类型都能互相转换，只有属于同一棵继承层次树中的引用类型才可以转换。

类型转换有两个方向：
* 将父类引用类型变量转换为子类类型，这种转换称为向下转型（downcast）；
* 将子类引用类型变量转换为父类类型，这种转换称为向上转型（upcast）。向下转型需要强制转换，而**向上转型是自动的**。

将父类引用赋值给子类变量时要进行强制转换，强制转换在编译时总是认可的，但运行时的情况取决于对象的值.如果父类对象引用指向的就是该子类的一个对象,则转换是成功的.否则会抛出`ClassCastException`. 如果不能确定实例是哪一种类型，可以在转型之前使用`instanceof`运算符判断一下。

## UML图简介
> UML是Unified Modeling Language的缩写，即统一标准建模语言。它集成了各种优秀的建模方法学发展而来的。UML图常用的有例图、协作图、活动图、序列图、部署图、构件图、类图、状态图。

面向对象分析与设计（OOAD）时，会用到UML图，其中类图非常重要，用来描述系统静态结构。Student继承Person的类图如图12-1所示。类图中的各个元素说明如图12-2所示，类用矩形表示，一般分为上、中、下三个部分，上部分是类名，中部分是成员变量，下部分是成员方法。实线+空心箭头表示继承关系，箭头指向父类，箭头末端是子类。UML类图中还有很多关系，如图12-3所示，如图虚线＋空心箭头表示实线关系，箭头指向接口，箭头末端是实线类。
![类图中的元素](https://upload-images.jianshu.io/upload_images/1662509-a3e3088cc59363cd.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
