## 内置数据类型

* **布尔型**（Boolean）
* **整型**（integer）
* **浮点型**（floating point）
* **字符**（character）



## 获取用户输入

```c++
#include<iostream>
#include<string>
using namespace std;
int main()
{
    cout<<"Please enter your name:";
    string user_name;
    cin>>user_name;
    return 0;
}
```

读取之前，我们需要先定义一个对象来存储数据，这包括数据类型和标识符。用于存储人名的类型，用int几乎不可能，更适当的类型是**标准库**中的**string**（**class**）

在使用数据类型string（class）之前还需要让程序知道该class的定义。故需要添加`#include<string>`。

`string user_name；`

接下来就可以利用已定义好的`cin`对象来读取用户在终端上的输入内容。通过input运算符`>>`将输入的内容定向到具有适当类型的对象身上。

`cin>>user_name;`

* **命名空间**

所谓命名空间（namespace）就是一种将**库名称封装**起来的方法，通过这种方法，可以避免和应用程序发生命名冲突的问题。`std`是标准库所驻命名空间的名称



## 对象初始化

一般来说，对每个对象初始化是个好习惯。常见的有两种初始化方法：**assignment**和**constructor syntax**。

* **赋值初始化（assignment）**

    即使用`=`运算符来进行初始化，沿袭自C语言，适用于**内置类型**或**对象可以单一值加以初始化**的情况。

    例如：`string sequence_name = 'Fibonacci';`

* **构造函数语法初始化（constructor  initialization syntax）**

    如果对象需要多个初值，赋值初始化就无法完成任务了。以标准库中的复数（complex number）为例，它就需要两个初值（实部和虚部）。有鉴于这种情况，于是引入了”多值初始化“的构造函数语法。

    ```C++
    #include<complex>
    complex<double> purei(0,7);
    ```

    出现在`complex`后面的尖括号`<>`表示`complex`是一个模板类（**template class**）。模板类允许我们在不必指明数据成员类型的情况下定义class。

    例如：在表示虚数时，这两个浮点数是用float、double、long double中的哪一个？模板类机制使程序员可以直到使用template class时才决定真正的数据类型。**程序员可以先插入一个代称，稍后再绑定实际数据类型**。上述代码中，将complex类的成员绑定至double类型。



## 表达式

例：希望每行打印的字符串不超过8个。

```C++
const line_size = 8;
int cnt = 1;
cout<<a_string<<(cnt % line_size ？ ' ' : '\n');
```



## 运算符优先级

以下运算符优先级依次递减，若想改变优先级可以使用小括号：

| **逻辑运算符** | ！           |
| :------------- | ------------ |
| 算术运算符     | *，/，%      |
| 算术运算符     | +，-         |
| 关系运算符     | >，<，<=，>= |
| 关系运算符     | ==，!=       |
| 逻辑运算符     | &&           |
| 逻辑运算符     | \|\|         |
| 赋值运算符     | =            |



## 条件语句与循环语句

1. 条件语句
    * **if**
    * **if-else**
    * **switch**（如果测试条件值属于整数类型，可以来替代大量if-else语句）
        * switch(表达式)：表达式的值必须是 整数形式
        * 之后是一组case标签，每个标签后是一个常量表达式：`case const_statement:`
        * switch后表达式被计算出后依次与case后表达式值比较，若符合则执行标签后的语句
        * 注意每个case标签后有无break语句，若没有则执行每条cas直到碰到default语句

2. 循环语句

    * **while**
        * 若在循环内遇到break语句，则循环结束；
        * continue语句用于终止当前迭代；

    * **for**

        ```C++
        for(init-statement;condition;expression)
            statement;//单一语句或语句块
        ```

        * expression会在每次迭代结束后被求值，通常用来改变两种对象的值：一是在init-statement中被初始化的对象，二是在condition中被检验的对象。



## 运用Array和Vector

> C++允许我们以**内置数组（array）**类型或标椎库提供的**vector**来定义容器。

例如：一个名为Pell的数组，包含18个整数元素

1. **array实现**

    ```C++
    const int seq_size = 18;
    int pell[seq_size];   //array的大小必须是常量表达式
    ```

    

2. **vector实现**

    ```C++
    #incluse<vector>
    vector<int> pell(seq_size);  //尖括号内指定其元素类型，大小写在小括号内，大小不一定得是常量表达式
    ```

    * 使用vector的注意事项：

        * vector是**模板类**

        * 必须包含vector**头文件**
        * **大小**不一定是常量表达式
        * 索引操作通过下标运算符`[]`实现
        * 第一个元素的位置是`0`



## 指针

一个未指向任何对象的指针，其**地址值为0**。有时候称之为**null指针**。此时利用`*`对指针解引用（dereference）会导致未知的执行结果。



# 2. 面向过程的编程风格

## 2.1 函数

例：指定序号，根据序号给出相应位置的Fabonacci数列的元素。input：8，output：21。

* 返回类型
* 函数名
* **参数列表**：扮演占位符（placeholder）的角色
* 函数体

函数必须先声明，才能被使用（调用）。函数声明得以让编译器检查后续使用方式是否正确（参数数量、类型等）。此即所谓的函数原型（function prototype）。

```C++
/*斐波那契数列，输入位置，给出该位置的值*/
int fibon_elem(int pos)
{
    cin>>pos;
    int elem = 1;
    int n_2 = 1;
    int n_1 = 1;
    for(int index = 3; index <= pos; ++index)
    {
        elem = n_2 + n_1;
        n_2 = n_1;
        n_1 = e
    }
    return elem;
}
```

* **函数调用**

    此处以一个正整数vector实现**冒泡排序（Bubble sort）**来举例（其中涉及传地址（by reference）和传值（by value））：

    

## 2.2 函数重载

## 2.3 函数模板

## 2.4 函数指针