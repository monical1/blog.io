---
layout: post
title: Java泛型(Generic)记录
date: 2017-08-03
categories: blog
tags: [Generic]
description: 这是第一篇利用Git Pages 记录的memo
---


## Generic deep dive

1. 上面代码能不能编译通过, 原因?
```` java
List<Object> list1 = new ArrayList<String>();
List<String> list2 = new ArrayList<Object>();
````
2. 泛型类能放哪些值, 只与reference有关
`List<Object> list = new ArrayList<Integer>()`

3. 泛型擦除的instance
```` java
ArrayList<String> arrayList1 = new ArrayList<String>();
arrayList1.add("abc");
ArrayList<Integer> arrayList2 = new ArrayList<Integer>();
arrayList2.add(123);
assertTrue(arrayList1.getClass() == arrayList2.getClass());
````

> `javap -c out\production\whatishell\com\monical\Pair.class`

类型擦除后, 只能存储Integer的集合List, 也能存储String, 下面为代码片段
````
public static void main(String[] args) throws IllegalArgumentException, SecurityException, IllegalAccessException, InvocationTargetException, NoSuchMethodException {
    ArrayList<Integer> arrayList3=new ArrayList<Integer>();
    arrayList3.add(1);// 这样调用add方法只能存储整形，因为泛型类型的实例为Integer
    arrayList3.getClass().getMethod("add", Object.class).invoke(arrayList3, "asd");
    for (int i=0;i<arrayList3.size();i++) {
        System.out.println(arrayList3.get(i));
    }
}
````
