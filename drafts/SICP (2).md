# SICP

## 第一章

什么是计算?

编程的基本元素:

- 基本表达式: 最简单的实体
- 组合的方法: 从简单的元素构建更复杂的元素
- 抽象的方法: 命名复合元素, 并像单元一样操纵

表达式

- 数字, 字符串, 符号(原子), 基本操作符等, 求值就是本身
- 复合表达式: 对表达式求值,就是将操作符应用到操作数
- 对变量求值: 返回环境中变量关联的值

组合表达式求值

1. 对组合表达式的子表达式求值
2. 将操作符应用到操作数

这个过程是递归的(EVAL-APPLY)

类似define这样的表达式称为特殊形式, 特殊形式有不同的求值规则.

lisp的求值规则包括一个通用的规则和一些特殊规则.

应用过程实际上就是替换约束出现的变量

cond/if 表达式是另一种特殊形式,cond表达式必须按需求值
cond 表达式传入 谓词-表达式对

完全展开并求值: 正则序
eval & apply: 应用序

在不引入变量,表达式有合法值的时候, 两种求值顺序得到相同的结果

因为and 和or 是短路求值的, 因此也需要特殊处理; 而not不需要



