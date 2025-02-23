# 关于C++

## C++的一些学习材料

- Itanium C++ ABI
    - https://itanium-cxx-abi.github.io/cxx-abi/abi.html
- cppreference
    - https://en.cppreference.com/
    - https://zh.cppreference.com/
- open-std
    - https://open-std.org/
- online draft
    - http://eel.is/c++draft/
- BS的首页
    - https://www.stroustrup.com/
- 几本书
    - C++ primer
    - The C++ Programming Language（TCPPL）
    - The Design and Evolution of C++
- 标准库实现
    - MSVC
    - LLVM
    - GCC

## C++的一些人

Bjarne Stroustrup

## 抄书

以下部分来自cppreference或者C++标准

C++ 程序是一个含有声明的文本文件序列。它们被翻译为一个可执行程序，程序在C++实现调用其主函数时被执行。
在C++程序中，一些被称为关键词的词语有着特殊的含义。其他词语可以被用作标识符。在翻译的过程中，注释会被忽略。C++程序也包含字面量，其中的字符的值由字符集与编码指定。程序中的某些特定字符必须通过转义字符表示。
C++程序中的实体包括值、对象、引用、结构化绑定（C++17起）、函数、枚举项、类型、类成员、模板、模板特化、包和命名空间。预处理宏不是C++实体。
声明可以引入实体，将它们与名字关联起来，并定义其属性。能够定义使用一个实体所需的所有属性的声明是定义。对任何被ODR使用的非内联函数或变量，程序中必须只有一个定义。
函数的定义通常包括一系列的语句，其中一部分会包含表达式。表达式指定了程序需要进行的运算。
程序中遇到的名字通过名字查找，与引入它们的声明关联起来。每个名字都只在称为其作用域的程序部分中有效。有些名字有链接，这使得它们即使出现在不同的作用域或翻译单元时，也代表相同的实体。
C++中的每一个对象、引用、函数和表达式都会关联一个类型，可以是基础类型，复合类型，或用户定义类型，以及完整或不完整类型等。
声明的不为非静态数据成员的对象和引用是变量。

C++程序可以创建、销毁、引用、访问并操作对象。
在C++中，一个对象拥有这些性质：
- 大小
- 对齐要求
- 存储期
- 生存期
- 类型
- 值
- 一个可选的名字

变量由声明引入，是对象或者是并非非静态数据成员的引用。

对象可以使用定义、new表达式、throw表达式、更改联合体的活跃成员和求值要求临时对象的表达式显式创建。显式对象创建完全定义了所创建的对象。

隐式生存期类型的对象也可以由以下操作隐式创建：
- 在常量求值以外的场合，开始类型unsigned char或std::byte的数组生存期的操作，此时在该数组中创建这种对象，
- 调用以下分配函数，此时在分配的存储中创建这种对象：
- 调用以下对象表示复制函数，此时在目标存储区域或结果中创建这种对象
- 调用下列特定的函数，此时在指定的存储区域中创建对象：

同一存储区域中可以创建零或多个对象，只要能给予程序有定义的行为即可。如果无法这样创建，例如操作冲突，那么程序行为未定义。如果多个这种隐式创建的对象的集合会给予程序有定义行为，那么不指定这些集合中的哪一个被创建。换言之，不要求隐式创建的对象是唯一定义的。

在指定的存储区域内隐式创建对象后，一些操作会生成指向已适当创建的对象的指针。已适当创建的对象与存储区域拥有相同地址。类似的，当且仅当不存在能给予程序有定义行为的指针时，行为才未定义；而如果有多个给予程序有定义行为的值，那么不指定产生哪个值。

调用std::allocator::allocate，或者联合体类型的隐式定义的复制/移动特殊成员函数，也能创建对象。

某些类型和对象具有对象表示和值表示，它们在下表中定义：

类型或对象的对象标识中不属于值表示的位是填充位。
对于可平凡复制类型，它的值表示是对象表示的一部分，这意味着复制该对象在存储中所占据的字节就足以产生另一个具有相同值的对象（除非该值是该类型的一个“陷阱表示”，将它读入到CPU中会产生一个硬件异常，就像浮点数的SNaN或整数的NaT
尽管大多数实现都不允许整数的陷阱表示、填充位或多重表示，但存在例外；例如Itanium上的整数类型值就可以是陷阱表示。
反过来不一定是对的：可平凡复制类型的两个具有不同对象补充的对象可能表现出相同的值。例如，浮点数有多种位模式都表示相同的特殊值NaN。更常见的是，会为了满足对齐要求和位域的大小等目的而引入填充位。
对于char，signed char和unsigned char类型的对象，除非它们是大小过大的位域，否则它的对象表示的每个位都参与它的值表示，而且每一种位模式都表示一个独立的值（没有填充位或陷阱位，不允许值的多种表示）

一个对象可以拥有子对象。子对象包括：
- 成员对象
- 基类对象
- 数组元素
不是其他任何对象的子对象的对象称为完整对象。
完整对象、成员对象和数组元素也被称为最终派生对象，以便和基类子对象区分开。
对于某个类，
- 它的非静态数据成员
- 它的非虚直接基类，以及
- 它不是抽象类时，它的虚基类。
被统称为该类的潜在构造的子对象。

如果一个子对象是基类子对象或者声明有`[[no_unique_address]]`属性的非静态数据成员，那么它是潜在重叠的子对象。
只有在满足以下所有条件时，对象obj的大小才有可能为零：
- obj是潜在重叠的子对象
- obj的类型是没有虚成员函数和虚基类的类类型
- obj没有非零大小的子对象，也没有非零长度的无名位域

对于满足以上所有条件的对象obj：
- 如果obj是没有非静态长远的标准布局类类型的基类子对象，那么它的大小为零
- 否则，由实现定义在哪些情况下obj的大小为零

任何非零大小的非位域对象都必须占据一个或更多字节的存储，其中包括它的子对象（全部或部分）占据的所有字节。如果对象具有可平凡复制或标准布局类型，那么占据的存储必须连续。

在很多情况下，通过类型与对象的创建类型不同的表达式来访问对象都是未定义行为，它的例子和例外参考reinterpret_cast。

每个对象类型都具有被称为对齐要求的性质，它是一个非负整数（类型是std::size_t，总是2的幂），表示这个类型的不同对象所能分配放置的连续相邻地址之间的字节数。

C++标准定义了两种实现：宿主（hosted）和独立（freestanding）实现。C++标准对宿主实现所规定的标准库标头集合比对独立实现所规定的大很多。独立实现中程序可能在没有操作系统的情况下运行。

实现的种类由实现定义。宏 __STDC_HOSTED__对宿主实现预定义为1，对独立实现为0.

针对多线程执行与数据竞争的规定

在独立实现下，程序能否拥有多于一个执行线程由实现定义。
在宿主实现下，C++程序可以拥有同时运行的多于一个线程。

针对main函数的要求
独立实现中，是否要求程序定义main函数是由实现定义的。启动与终止过程是由实现定义的。启动过程中包含执行具有静态存储期的命名空间作用域对象的构造函数；终止过程三包含执行具有静态存储期的对象的析构函数。
宿主实现中，程序必须包含一个名为main的全局函数。程序执行时启动一个主执行线程，在其中调用main函数。并且具有静态存储期的变量将在其中被初始化和销毁。

针对标准库标头的规定
独立实现拥有由实现定义的标头集合。此集合至少包含下表中的标头。
对于部分独立的标头，独立实现只需要提供对应概要中的部分实体：
- 如果实体备注为独立，那么保证会提供它。
- 如果实体备注为独立或被删除，那么保证会提供或删除它

## C++ 具名要求

确保以满足这些要求的模板实参实例化标准库模板是程序员的重担。若不这么做，则可能导致非常复杂的编译器诊断。

- 基本概念
    - 可默认构造：指定可以默认构造该类型的对象
    - 可移动构造：指定可以从右值构造该类型的对象
    - 可复制构造：指定可以从左值构造该类型的对象。
    - 可移动赋值：指定可以从右值对该类型的对象赋值
    - 可复制赋值：指定可以从左值对该类型的对象赋值
    - 可析构：知名可以销毁该类型的对象
- 类型属性
    - 标量类型：不是数组类型或类类型的对象类型
    - 简旧数据类型：POD结构体，与C的struct兼容
    - 可平凡复制：这些类型的对象能够在复制底层字节后保持原值
    - 平凡类型：这些类型的对象可以被平凡地构造和复制
    - 标准布局类型：这些类型适用于与其他语言编写的代码交流
    - 隐式生存期类型：这些类型的对象可以被隐式创建，它们的生存期也可以隐式开始

## 伪析构函数

https://zhuanlan.zhihu.com/p/410232329

```c++
typedef int Int;
int x;
1.~Int();           // no, 词法分析，1.解析为浮点字面量
x.~int();           // no，~后需要接类型名或者decltype说明符，不能接关键字
(1).~Int();         // ok
x.~Int();           // ok
x.~decltype(x)();   // ok, C++11
```

## 对齐

## C++类型

- 基础类型
    - void类型
    - std::nullptr_t类型
    - 算术类型
        - 整数类型
            - bool类型
            - 字符类型
                - 窄字符类型
                    - 普通字符类型：char，signed char，unsigned char （注意signed char，unsigned char是窄字符类型，但不是字符类型；也就是说窄字符类型不是字符类型的子集）
                    - char8_t类型
                - 宽字符类型：char16_t, char32_t,wchar_t
            - 有符号整数类型
                - 标准有符号整数类型：signed char, short int，int, long int, long long int
                - 扩展有符号整数类型（由实现定义）
            - 无符号整数类型
                - 标准无符号整数类型: unsigned char, unsigned short int, unsigned int, unsigned long int, unsigned long long int
                - 扩展无符号整数类型（与扩展有符号整数类型一一对应）
        - 浮点数类型
            - 标准浮点数类型：float，double，long double
            - 扩展浮点数类型
                - 定宽浮点数类型
                - 其他由实现定义的浮点数类型
- 复合类型
    - 引用类型
        - 左值引用类型
        - 右值引用类型
    - 指针类型
        - 对象指针类型
        - 函数指针类型
    - 成员指针类型
        - 指向数据成员的指针类型
        - 指向成员函数的指针类型
    - 数组类型
    - 函数类型
    - 枚举类型
        - 无作用域枚举类型
        - 有作用域枚举类型
    - 类类型
        - 非联合体类型
        - 联合体类型

C++的类型分为基础类型和复合类型。

基础类型实际上就只有三种：void类型，std::nullptr_t类型和算术类型。
算术类型包括整数类型和浮点数类型。
整数类型包括bool类型，字符类型，有符号整数类型和无符号整数类型。
字符类型包括窄字符类型和宽字符类型。
窄字符类型包括普通字符类型（char, unsigned char, signed char）和char8_t类型
宽字符类型包括char16_t,char32_t,wchar_t
复合类型包括引用类型，指针类型，成员指针类型，数组类型，函数类型，枚举类型和类类型。

## RAII

RAII，即资源获取即初始化

## std::enable_if

```c++
template<bool B,class T = void>
struct enable_if{};

template<class T>
struct enable_if<true,T> {typedef T type;};
```

如果B为true，则std::enable_if拥有公开成员typedef的type T；否则，无成员typedef

当我们需要使用类型T的时候，用std::enable_if_t<expr, T>替换,如果expr求值为true，可以推导出T，否则触发SFINAE，从重载决议中去除。

## char, unsigned char, signed char

同时承担三种任务：寻址单元，算术类型和字符类型。

寻址单元应该使用std::byte，算术类型应该使用定长类型比如uint8_t, 剩下的责任只有字符类型

## byte的实现

对多种类型的辨析详见：https://stackoverflow.com/q/77097673

byte可以实现为有作用域枚举，也可以实现为其他类型的别名。

byte代表寻址单元，但没有整数类型的功能，byte可以进行位运算，但不能进行普通代数运算。

## std::move 和 std::forward

## 宽字符和多字节字符的区别

多字节也就是变长编码，宽字符就是将一个字符存放在一个定长对象中。

问题出在unicode出现的早期，ms误将宽字符长度定为16位，然而16位实际上不足以存放所有字符。

## UCS-2和UTF-16的区别

UCS-2: 仅以2字节存储的，码位小于U+FFFF的Unicode字符。

## 模板的实例化、特化和偏特化

## 一些问题

- C++中的对象和面向对象编程中的对象含义的区别
- 不考虑兼容问题的情况下，对C++做哪种更改，会让C++更好
- C++标准引入对象表示和值表示的原因
- 对象与存储的关系，为什么一个非子对象必须占据存储。
- 移动语义窃取资源，似乎是对无法直接交换对象的存储的一种变通手段
- SFINAE的使用方法
- RAII的真实含义

