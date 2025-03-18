---
title: List对象排序
cover: /img/cover/4.jpg
hide: false
date: 2024-06-19 13:53:16
permalink: java/collections-sort.html
tags:
 - java
 - list
 - sort
categories: 
 - Java
keywords:
description:
top_img:
comments:
toc:
toc_number:
toc_style_simple:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
abcjs:
---

### 前言

记一下Java中List对象的三种排序方式，万一用得着呢（已经用着了）。

---

### 方案一

简单对象排序，如Integer对象，String对象等，代码如下：

```java
// 调用Collections.sort 方法
public class SortTest {

    public static void main(String[] args) {

        List<Integer> integerList = new ArrayList<>();
        integerList.add(9);
        integerList.add(4);
        integerList.add(6);
        integerList.add(1);
        integerList.add(8);
        integerList.add(7);
        integerList.add(5);
        // 默认升序
        Collections.sort(integerList);
        for (Integer i : integerList){
            System.out.println(i);
        }
        // 设置为降序
        Collections.sort(integerList,Collections.reverseOrder());
        for (Integer i : integerList){
            System.out.println(i);
        }
    }
}
```

```java
// 调用List.sort()方法，传入对象compareTo方法，一般不用该方法排序简单对象
public class SortTest {
    public static void main(String[] args) {
        List<Integer> integerList = new ArrayList<>();
        integerList.add(9);
        integerList.add(4);
        integerList.add(6);
        integerList.add(1);
        integerList.add(8);
        integerList.add(7);
        integerList.add(5);
        integerList.sort(Integer::compareTo); //方法名可以自定义，建议遵循java命名规则
        for (Integer i : integerList){
            System.out.println(i);
        }
    }
}
```



### 方案二

自定义对象排序，可重写compareTo方法排序

```java
public class SortTest {

    public static void main(String[] args) {

        List<User> integerList = new ArrayList<>();
        integerList.add(new User("m",9));
        integerList.add(new User("j",4));
        integerList.add(new User("y",6));
        integerList.add(new User("q",1));
        integerList.add(new User("i",8));
        integerList.add(new User("b",7));
        integerList.add(new User("d",5));
        integerList.sort(User::compareTo);
        for (User i : integerList){
            System.out.println("name:" + i.getName() + ",sex:" + i.getSex());
        }
    }
}

class User{
    private String name;

    private Integer sex;

    public User(String name, Integer sex){
        this.name = name;
        this.sex = sex;
    }

    public User(){}

    public int compareTo(User user){
      	// 这里设置为升序，
      	// 降序写法替换顺序：user.getSex().compareTo(this.getSex()); 
        return this.getSex().compareTo(user.getSex()); 
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getSex() {
        return sex;
    }

    public void setSex(Integer sex) {
        this.sex = sex;
    }
}
```

### 方案三

用匿名函数重写排序方法

```java
public class SortTest {

    public static void main(String[] args) {

        List<User> integerList = new ArrayList<>();
        integerList.add(new User("m",9));
        integerList.add(new User("j",4));
        integerList.add(new User("y",6));
        integerList.add(new User("q",1));
        integerList.add(new User("i",8));
        integerList.add(new User("b",7));
        integerList.add(new User("d",5));
        integerList.sort(new Comparator<User>() { // 这个在java8中可以用表达式写：(t1,t2) -> t1.getSex() >= t2.getSex() ? 1 : -1;
            @Override
            public int compare(User o1, User o2) {
                return o1.getSex() >= o2.getSex() ? 1 : -1; //这里升序为1:-1，降序为-1:1
            }
        });
        for (User i : integerList){
            System.out.println("name:" + i.getName() + ",sex:" + i.getSex());
        }
    }
}

class User{
    private String name;

    private Integer sex;

    public User(String name, Integer sex){
        this.name = name;
        this.sex = sex;
    }

    public User(){}

    public int compareTo(User user){
        return user.getSex().compareTo(this.getSex());
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getSex() {
        return sex;
    }

    public void setSex(Integer sex) {
        this.sex = sex;
    }
}
```

