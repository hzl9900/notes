# 关于C++

## C++的一些学习材料

- Itanium C++ ABI
    - <https://itanium-cxx-abi.github.io/cxx-abi/abi.html>
- cppreference
    - <https://en.cppreference.com/>
    - <https://zh.cppreference.com/>
- open-std
    - <https://open-std.org/>
- online draft
    - <http://eel.is/c++draft/>
- BS的首页
    - <https://www.stroustrup.com/>
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
在C++中，一个对象拥有这些性质

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

<https://zhuanlan.zhihu.com/p/410232329>

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
                    - 普通字符类型：char，signed char，unsigned char
                    -（注意signed char，unsigned char是窄字符类型，但不是字符类型；也就是说窄字符类型不是字符类型的子集）
                    - char8_t类型
                - 宽字符类型：char16_t, char32_t,wchar_t
            - 有符号整数类型
                - 标准有符号整数类型：signed char, short int，int, long int, long long int
                - 扩展有符号整数类型（由实现定义）
            - 无符号整数类型
                - 标准无符号整数类型: unsigned char/short/int/long int/long long int
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

对多种类型的辨析详见：<https://stackoverflow.com/q/77097673>

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

## C++ 相对于 C的新增内容

- 新增数据类型
- 类/用户定义类型(user define type)
- 多态
    - 特设多态(ad hoc): 函数重载, 操作符重载
    - 参数多态: 模板
    - 子类型多态: 继承
- 模板
- 异常
- 命名空间
- 操作符重载
- 函数名重载
- 引用
- 内存管理: new/delete 操作符
- 新增库设施

## C++ 实现对程序的反应

- 对一个正常的程序，合规的实现应该接受并正确执行程序，除非超出了实现本身的限制
- 如果程序包含对一条规则的限制，而这条限制不要求诊断，标准对实现没有要求
- 如果程序
    - 违反了需要诊断的规则
    - 某个预处理翻译单元包含#warning 指令
    - conditionally-supported, 但是实现不支持这个construct
    - 此时实现应该至少提出一条诊断信息

## C++ 的翻译阶段 (phase of translation)

C++ 标准不要求实现严格按照执行，但是需要遵守如同规则。

一共九个阶段

1. 映射源字符
2. 拼接行
3. 词法分析
4. 预处理
5. 确定字符串字面量的公共编码
6. 拼接字符串字面量
7. 编译
8. 实例化模板
9. 链接

## C++的内置类型转换

- _ -> 布尔：0为false，其他为true
- 布尔 -> _: false为0, 其他为1
- 浮点->整数: 截断
- 整数->浮点: 小数部分为0, 浮点数超出范围可能有精度损失
- 无符号整数赋值超出范围: 取模
- 有符号整数赋值超出范围: UB

TODO: 区分赋值和运算
TODO: 为什么给有符号整数赋值超过范围是UB而不是取模

## 字面量的类型

- 整数
- 浮点数
- 布尔
- 指针
- 字符
- 字符串

## 关于标识符

以下标识符被保留

- 在全局命名空间中，以单个下划线开头的标识符
- 除特殊情况外，以双下划线或者单下划线跟随一个大写字母的标识符

被保留的意思是，标准库或者编译器会假定这样的标识符是未被使用的，如果程序员使用这样的标识符的话，程序IFNDR

## C++的歧义

TODO

## class 与 struct 的区别

class 成员和继承默认private， struct 默认public

class 可以用于模板参数声明 `template<class T>`

## C++的初始化

- `string s1;`
- `string s2(s1)`
- `string s3=s1`
- `string s4("string")`
- `string s5="string"`
- `string s6('c', 10)`

根据初始化器的语法可以分为复制初始化，列表初始化，直接初始化（C++11起）

如果不指定初始化器，对象会默认初始化
如果为对象指定的初始化器是()，则对象会值初始化
如果为引用指定的初始化器是(), 则程序IF

初始化器的语义：

- 如果初始化引用，参考引用初始化
- 如果初始化对象，给定类型为T
    - 如果使用 =， 对象会复制初始化
    - 如果使用 {}或者={}，则对象会列表初始化
    - 如果使用（），则对象会直接初始化

值初始化：空初始化器

- `T obj();`
- `T obj{};`
- `new T()`

值初始化的效果：

- 如果T是类类型
    - 如果T默认初始化选择了一个构造函数，并且由用户提供，那么对象首先被零初始化
    - 任何情况下，对象都被默认初始化
- 如果T是数组类型，值初始化数组的每一个元素
- 否则，零初始化对象

注：语法`T obj();`声明一个不接收参数，并返回T的函数，在C++11之前，使用`T obj = T()`,这里值初始化一个临时对象并复制初始化，多数编译器可以优化掉复制。

默认初始化：不使用初始化器

- `T obj;`
- `new T`

默认初始化的效果：

- 如果T是类类型，那么考虑各构造函数并实施针对空实参列表的重载决议，调用所选的构造函数，以提供新对象的初始值
- 如果T是数组类型，那么该数组的每个元素都被默认初始化
- 否则不进行初始化

零初始化：将一个对象的初始值设为零
零初始化在语言中没有专用语法。

零初始化的效果：

- 如果T是标量，对象的初始值是将整数字面量0显式转换到T的值
- 如果T是非联合体类类型，那么
    - 初始化所有填充位为0
    - 零初始化所有非静态数据成员
    - 零初始化所有非虚基类子对象
    - 如果对象不是基类子对象，那么也零初始化所有虚基类子对象
- 如果T是联合体类型
    - 初始化所有填充位为零位
    - 零初始化对象的首个非静态具名数据成员
- 如果T是数组类型，那么零初始化每个元素
- 如果T是引用类型，那么不做任何事

注：`T obj = T();`直接初始化+复制初始化,  而`T obj = T{}`是列表初始化.

## *和.的优先级

`*p.f()` 中 `.` 的优先级更高,因此为 `(*p).f()` 创建了别名 `p->f()`

## MVP(Most Vexing Parsing)

TODO

## C++的取余

TODO

## C++的sizeof 运算符

## C++的显式转换

- C风格的类型转换
- C++风格的类型转换
    - static_cast
    - dynamic_cast
    - const_cast
    - reinterpret_cast

static_cast: 任何有明确定义的类型转换，只要不包括底层const，都可以使用static_cast

## C++的变量和对象

TODO

## switch语句与if语句的区别

TODO

## 实参和形参的关系

实参是形参的初始值，标准没有规定实参的求值顺序

要定义一个没有形参的函数，可以用空的形参列表，为了与C语言兼容，也可以用(void)

函数的返回类型不能是数组类型或者函数类型。

形参名是可选的，但是我们无法使用未命名的形参，所以形参一般都应该有个名字。这里指的是函数定义，函数声明由于不包括函数体，所以无须形参的名字。

函数的三要素(返回类型，函数名，形参类型)  描述了函数的接口，说明了调用该函数所需的全部信息。函数声明也称为函数原型。

函数也应当在头文件中声明，而在源文件中定义

## 头文件与源文件的区别

TODO

## 参数传递

如果形参是引用类型，将绑定到对应的实参上，否则将实参的值拷贝后赋予形参。

当形参是引用类型时，称实参被引用传递或者函数被传引用调用，当实参的值被拷贝时，称实参被值传递，或者函数被传值调用

C++在传入实参时不需要标注call by reference/value。和rust不同

C++可以利用引用返回值。

形参的初始化方式和变量的初始化方式是一样的。

在不必要的时候，应该尽量使用常量引用，避免错误的修改传入变量

## 函数匹配

候选函数：

- 与被调用的函数同名
- 声明在调用点可用

可行函数

- 形参数量与实参数量相等
- 实参类型与形参类型相同，或者可以转换为形参的类型
- 该函数每个实参的匹配都不劣于其他可行函数需要的匹配
- 至少有一个实参匹配优于其他可行函数提供的匹配

## 匹配程度分级

- 精确匹配
    - 相同
    - 数组/函数退化为指针
    - 顶层const
- const转换
- 类型提升
- 算术类型转换或者指针转换
- 类类型转换

优先匹配非常量引用/指针

## 类的两步处理

首先编译成员的声明，然后才是编译成员函数体。

因此成员函数体可以使用类中的其他成员。

TODO 为什么C++隐式使用类成员，而不使用this.name

## 自由空间(free store)和堆的区别

??? 自由空间是C++的说法，堆则是C语言的说法，区别只存在于标准的wording上，实质是一个东西。问题出在C语言中malloc，free和C++中new delete的交互上。

malloc/free属于标准库,而new,delete属于语言核心

## placement new的用途

## std::launder, std::start_lifetime_with

## 函数是否应该返回std::unique_ptr

## RAII 和 scope based memeory management

## weak_ptr 通过lock获取shared_ptr

## ADL的用途

```C++
using std::swap;
swap(lhs.h, rhs.h);
```

## 为什么不能使用T&,而是使用const T&和T&&

## 为什么使用运算符重载, 而不是函数重载

遵守C++的约定

## 为什么需要虚析构函数

## unique_ptr和shared_ptr deleter的区别

重载shared_ptr的deleter很方便,相反的,deleter类型是unique_ptr类型的一部分.

## legacyIterator

只是C++ reference 的写法, 与ranges的iterator区分, 标准中不是这么写的...

## 指针占用的大小

取决于平台(包括操作系统,编译器和硬件)

多种约定

32位系统上通常是4字节,64位系统上通常是8字节.

??? 目前64位系统并没有真正使用64位地址空间,似乎最多使用到52位

## 整数类型的长度

## 解释C++中的封装,  继承和多态性

## C++中的多种多态

多态(polymorphism)

- 特设多态: 包括函数重载,运算符重载
- 参数多态: 模板
- 子类型多态: 继承

理论上宏也可以实现多态

## explicit的用途

防止类构造函数的意外调用

## 什么是虚函数,为什么在基类中使用虚函数

## 如何处理内存泄漏问题,常见的内存管理技术

## 堆和栈的区别

这个问题实际上不是C++范畴的问题

## 什么是析构函数,有什么用?

## const关键字的作用

## 引用和指针的区别

## C++11的新特性有哪些? 你觉得哪个有用?

## 深拷贝和浅拷贝

## 什么是运算符重载,C++中的使用场景

## 解释模板类和模板函数, 给出示例代码

## C++中的异常处理机制,应该怎么用

## STL库中的常用容器, 包括vector, list, map

## STL库中的迭代器

## C++中的命名空间的概念及其作用

## 静态成员变量和静态成员函数

## C++ static 关键字的用途

## C++中*,&的用途

## 预处理器在C++中的作用, 常见用法

## 文件读写操作

## 指针和数组的关系

## C++中常用的设计模式

## C++11后的线程

## 什么是Lambda表达式

## auto关键字的作用

## 什么是智能指针, 常见的智能指针类型,特点和适用场景

## C++的char类型

## 什么是隐式可移动实体
