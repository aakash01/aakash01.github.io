---
layout: post
title: "Final Keyword And Immutable Classes"
description: "Final Keyword in Java"
category: Java
tags: [Java]
published: true
author: aakash01
---
{% include JB/setup %}

**Final Variable**

A variable declared final can't be modified. So final variables are by default read-only. 

- Final Variables improves performance as they can be cached. 

- Final variables are thread-safe. 

**Final Method**

A method declared final can't be overridden.  Final methods are faster as they do not require to be resolved
during runtime. 

**Final Class**

Final Class is a class which can't be sub-classed. 

Eg: String. 



**Final Keyword helps to write Immutable Classes**. 

Few Points on final keyword. (From javarevisited)

1. Final keyword can be applied to member variable, method or class. 


2. Final member variable must be initialized at the time of declaration or inside of constructor. 

3. You cannot reassign a value to final keyword. 

4. local final variable must be initialized during declaration. 

5. Only final variable / Effective Final(java8) is accessible inside anonymous class. 

6. Final methods can't be overridden. 

7. All variables declared inside interface are final. 


8. Final Methods are bonded during compile time, called as static binding. 


9. Making a class, method or variable final can improve performance as JVM can make assumptions and optimizations. 

10. Making a collection variable final means only the reference can't be changed, but the collection can be modified.
 
Eg: 

``` java
private final List list = new ArrayList<>();
list.add("Item1"); // OK
list.add("Item2"); // OK
list = new ArrayList<>(); // ERROR.
```

--------------------------------------------------------------




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
 {% highlight java %}
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


**Template for creating immutable objects.**

    Make all fields private
    Don't provide mutators
    Ensure that methods can't be overridden by either making the class final (Strong Immutability) or making your methods final (Weak Immutability)
    If a field isn't primitive or immutable, make a deep clone on the way in and the way out. 

[Preferred Reading ](http://www.javaranch.com/journal/2003/04/immutable.htm)


*************

**************
