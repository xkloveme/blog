---
title: javascript逻辑运算符“||”和“&&”的简单梳理
date: 2018-05-31 23:28:19
tags: [技术]
categories: 前端
---

一道经典的前端面试题：

> alert(1 && 2) 得到的结果是什么？ A:true      B:false      C:1      D:2

请带着你的回答，往下看…… 那么 alert(1||''&&2)的结果呢？？

## 逻辑或

逻辑或,也就是“||”。从字面上来说，只有前后都是 false 的时候才返回 false，否则返回 true。

1.  alert(true||false);    // true
2.  alert(false||true);    // true
3.  alert(true||true);        // true
4.  alert(false||false);    // false

更加深一点的

1.  alert(0||1);  //1
2.  alert(2||1);  //2
3.  alert('a'||1); //'a'
4.  alert(''||1);//1
5.  alert('a'||0);// 'a'
6.  alert('a'||'b');// 'a'
7.  alert(''||0);// 0
8.  alert(0||'');//''

**这就意味** 1、只要“||”前面为 false,不管“||”后面是 true 还是 false，都返回“||”后面的值。 2、只要“||”前面为 true,不管“||”后面是 true 还是 false，都返回“||”前面的值。

## 逻辑与

下面说说逻辑与（&&）,从字面上来说，只有前后都是 true 的时候才返回 true，否则返回 false。

1.  alert(true&&false);    // false
2.  alert(true&&true);    // true
3.  alert(false&&false);    // false
4.  alert(false&&true);    // false

同样的

1.  alert(0&&1);  //0
2.  alert(2&&1);  //1
3.  alert('a'&&1); //1
4.  alert(''&&1);//''
5.  alert('a'&&0);// 0
6.  alert('a'&&'b');// 'b'
7.  alert(''&&0);// ''
8.  alert(0&&'');//0

**这意味着** 1、只要“&&”前面是 false，无论“&&”后面是 true 还是 false，结果都将返“&&”前面的值; 2、只要“&&”前面是 true，无论“&&”后面是 true 还是 false，结果都将返“&&”后面的值; 让我们总结一下： 1、只要“||”前面为 false，无论“||”后面是 true 还是 false，结果都返回“||”后面的值。 2、只要“||”前面为 true，无论“||”后面是 true 还是 false，结果都返回“||”前面的值。 3、只要“&&”前面是 false，无论“&&”后面是 true 还是 false，结果都将返“&&”前面的值; 4、只要“&&”前面是 true，无论“&&”后面是 true 还是 false，结果都将返“&&”后面的值; 由上两个测试可知，逻辑运算符，“||”和“&&”都是遵行短路原则，只要确定符号前面的真假，既可确定返回值。 **简单点来说，&&相当于 if，如果前面为 true 则进行下一步输出后面的值不为真则返回本身，||刚好和&&相反** 另外说明&&优先级高于||，所以上面的值为 2 和 1，亲爱的你做对了么？
