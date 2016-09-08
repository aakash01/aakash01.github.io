---
layout: post
title: "Dive into Java   Part 1"
description: ""
category: 
tags: []
---
{% include JB/setup %}

> OOPs Concepts in Java

### Polymorphism

	It is the ability of one method to have different behaviour depending on the the type of object it is being called upon OR the type of object passed as argument.

	1. Runtime Polymorphism : Eg. Method Overriding
	2. Compiletime polymorphism : Eg. Method Overloading

**Method Overloading** is when two or more method in a class have same name but different parameters. 

 *	Java uses *static binding* to select appropriate method at compile time. 
 *	It uses Type(class) to resolve binding.

Eg: 

``` java
public static double Math.max(double a, double b){..}
public static float Math.max(float a, float b){..}
```

**Method Overriding** is when we redefine a method from base class to its child class . The Overridden method have same declaration but different definition. 

*	Java uses *dynamic binding* to bond overridden methods at runtime. 
*	It uses Object to resolve binding. 
*	Virtual methods are bonded by dynamic binding (**Virtual Methods** : All the non static methods are Virtual Methods. Only methods marked with the keyword final, which cannot be overridden, along with private methods, which are not inherited, are non-virtual).

Eg:

``` java
public class Animal {
    public void makeNoise()
    {
        System.out.println("Some sound");
    }
} 
class Dog extends Animal{
    public void makeNoise()
    {
        System.out.println("Bark");
    }
} 
class Cat extends Animal{
    public void makeNoise()
    {
        System.out.println("Meawoo");
    }
}
```

``` java
public class Demo
{
    public static void main(String[] args) {
        Animal a1 = new Cat();
        a1.makeNoise(); //Prints Meowoo
         
        Animal a2 = new Dog();
        a2.makeNoise(); //Prints Bark
    }
}
```







