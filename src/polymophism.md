# 编程中的多态

## 更新记录

## 多态的定义

1967年，Christopher Strachey 在 Fundmental Concepts in Programming Languages 3.6.4 节中提出多态的概念。

## 多态的分类

- 特设（ad hoc）多态
- 参数多态
- 子类型多态

### 特设多态

一个多态函数可以应用于不同类型的实际参数上，但是根据参数类型不同，有不同的表现。（常被称为 函数重载/运算符重载）

注意特设意味这多态函数对不同参数可能有完全不同的行为。

```C++
double add_one_or_multiply_two(double x) {
    return 2.0 * x;
}
int add_one_or_multiply_two(int x) {
    return x + 1;
}
```

上面举的例子可以看出，对于不同的类型，行为可能完全无关。

### 参数多态

参数多态允许我们传入类型作为参数，有时被称为泛型。

举一个rust book中的例子

```rust
fn largest<T>(list: &[T]) -> &T
    where T: std::cmp::PartialOrd{
    let mut largest = &list[0];

    for item in list {
        if item > largest {
            largest = item;
        }
    }

    largest
}

fn main() {
    dbg!(largest(&[1,2,3,4,5])); // 5
}
```

注意这里还给T增加了限定。

### 子类型多态

这里给出一个C++的例子

```C++
struct Animal {
  virtual void talk() const = 0;
};

struct Cat : public Animal {
  void talk() const { cout << "Meow" << endl; }
};

struct Dog : public Animal {
  void talk() const { cout << "Woof" << endl; }
};

void hear(const Animal &animal) { animal.talk(); }

int main() {
  Cat cat;
  Dog dog;
  hear(cat);
  hear(dog);
}
```

这里的子类型多态利用虚函数实现，是动态的。

下面给出CRTP的实现，程序在编译器就可以确定类型。

```C++
template <class T>
struct Animal {};

struct Cat : public Animal<Cat> {
  void talk() const { cout << "Meow" << endl; }
};

struct Dog : public Animal<Dog> {
  void talk() const { cout << "Woof" << endl; }
};

int main() {
  Cat cat;
  Dog dog;
  cat.talk();
  dog.talk();
}
```

## 参考资料

[中文维基](https://zh.wikipedia.org/wiki/%E5%A4%9A%E6%80%81_(%E8%AE%A1%E7%AE%97%E6%9C%BA%E7%A7%91%E5%AD%A6))
Christopher Strachey 《Fundmental Concepts in Programming Languages》
