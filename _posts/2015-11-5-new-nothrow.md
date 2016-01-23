---
layout: post
title: new与 new(std::nothrow)
categories: C++
tags: C++
---

###  C++ new与new (std::nothrow)

---

- new (std::nothrow) 
顾名思义，即不抛出异常，当new一个对象失败时，默认设置该对象为NULL，这样可以方便的通过if(p == NULL) 来判断new操作是否成功

- new
普通的new操作，如果分配内存失败则会抛出异常，虽然后面一般也会写上if(p == NULL) 但是实际上是自欺欺人，因为如果分配成功，p肯定不为NULL；而如果分配失败，则程序会抛出异常，if语句根本执行不到。

因此，建议在c++代码中，凡是涉及到new操作，都采用new(std::nothrow)，然后if(p==NULL)的方式进行判断
