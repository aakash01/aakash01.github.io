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




