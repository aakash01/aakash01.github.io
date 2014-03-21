---
layout: post
title: "Dive into Java   Part 1"
description: ""
category: 
tags: []
---
{% include JB/setup %}



> What is immutable object in java? How can we write one?

**Immutable classes** are those classes whose object can not be modified once created, ie any alteration to immutable object will result in creation of new object. Example String.
 
Benefits,

1. Provide Concurrency and multithreading advantages. Immutable objects are by default `thread safe` and can be shared without synchronization in concurrent environment.
2. Reusability : Immutable objects can be cached and reused.

Disadvantages,

1. Expensive, if you frequently need to modify data as everytime a new object gets created.
2. Reflection based frameworks are complicated by immutable objects since they requires constructor injection

To Write Immutable Object

1. All the fields must be private and preferably final
2. Don't provide any setters for the fields ie `no mutators`.
3. We need to make sure methods cannot be overridden

	* **Strong Immutability** : Make the Class final so cannot be overriden.

	* **Weak Immutability** : Make methods final and use static factories, keep constructors private. Eg If class A is weakly immutable, then a class B extending A will be partially immutable ie only behaviour defined by A will be immutable.
4. Protect mutable fields 
5. Watch out for collections. Use Collections.unmodifiable. Also, collections should contain only immutable Objects.
6. Don't provide any methods that change the internal state of the Object
 	Eg : 
 {% highlight java linenos %}
 import java.util.Date;
 public final class Person
 {
 	private String name;
 	private Date dob;   // mutable object
 	public Person( String name,Date dob)
 	{
 		this.name = name;
 		this.dob = new Date( dob.getTime() );    // Take a copy of date instance rather than trusting the reference
 	}
 	public String getName()
 	{
 		return this.name;
 	}
 	public Date getDOB(){	
 		return (Date) this.dob.clone();          // Return a copy of original object
 	}
 	
 }
 {% endhighlight %}
 	
	 So All the getters must provide immutable objects or use defensive(deep) copying. 

[Preferred Reading ](http://www.javaranch.com/journal/2003/04/immutable.htm)


*************

**************

> OOPs Concepts in Java

###Polymorphism

	It is the ability of one method to have different behaviour depending on the the type of object it is being called upon OR the type of object passed as argument.

	1. Runtime Polymorphism : Eg. Method Overriding
	2. Compiletime polymorphism : Eg. Method Overloading

**Method Overloading** is when two or more method in a class have same name but different parameters. 

 *	Java uses *static binding* to select appropriate method at compile time. 
 *	It uses Type(class) to resolve binding.

Eg: 
 {% highlight java linenos %}
 public static double Math.max(double a, double b){..}
 public static float Math.max(float a, float b){..}{% endhighlight %}

**Method Overriding** is when we redefine a method from base class to its child class . The Overridden method have same declaration but different definition. 

*	Java uses *dynamic binding* to bond overridden methods at runtime. 
*	It uses Object to resolve binding. 
*	Virtual methods are bonded by dynamic binding (**Virtual Methods** : All the non static methods are Virtual Methods. Only methods marked with the keyword final, which cannot be overridden, along with private methods, which are not inherited, are non-virtual).

Eg:
{% highlight java linenos %}
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
{% endhighlight %}
{% highlight java linenos %}
public class Demo
{
    public static void main(String[] args) {
        Animal a1 = new Cat();
        a1.makeNoise(); //Prints Meowoo
         
        Animal a2 = new Dog();
        a2.makeNoise(); //Prints Bark
    }
}
{% endhighlight %}







