---
layout: post
title: "Dive into JAVA Part 3"
description: "Reflection"
category: 
tags: []
---
{% include JB/setup %}

>What is Reflection? 
When you look in a mirror:
- You can see your reflection
- You can act on what you see


<blockquote class="blockquote-reverse">
<p class="text-muted">
In computer programming: Reflection provides ability to inspect and modify the runtime behavior of applications.Its consists of 2 things:
<ol>
<li> <kbd>Metadata - data about data i.e about class, constructor, method, fields, etc</kbd><br/>
<li> <kbd>Manipulate the metadata.</kbd><br/>
		</li>
		</ol>
</p>
</blockquote>

It’s important to note that reflection specifically applies to objects – so you need an object of a class to get information for that particular class. 
**Retrieving Class Objects**
The entry point for all reflection operations is java.lang.Class. There are several ways to get a Class depending on whether the code has access to an object, the name of class, a type, or an existing Class.
1. Object.getClass()    
eg: "foo".getClass()  - returns Class for String, System.console().getClass() - returns java.io.Console class.
2. The .class Syntax  - used mainly for primitive type.
eg: boolean.class will return the boolean class
3. Class.forName() - cannot be used for primitive types

Eg: 
{% highlight java %}
public class RefleactionDemo {
public static void main(String args[]){
System.out.println( "foo".getClass() + "   " + System.console().getClass() );
System.out.println(boolean.class);
Class c = Class.forName("java.lang.Class");
System.out.println(c.isArray());    
/* 
 Class c = Class.forName(“[B”); // byte[]
Class c = Class.forName(“[[B”); // byte[][] */

}
}

Output:
class java.lang.String  class java.io.Console
boolean
false
{% endhighlight %}


Java stores metadata in classes
- Metadata for a class: java.lang.Class
- Metadata for a constructor: java.lang.reflect.Constructor
- Metadata for a field: java.lang.reflect.Field
- Metadata for a method: java.lang.reflect.Method
{% highlight java %}
class Class {
Constructor[] getConstructors();
Field getDeclaredField(String name);
Field[] getDeclaredFields();
Method[] getDeclaredMethods();
...
}
class Field {
Class getType();
...
}
class Method {
Class[] getParameterTypes();
Class getReturnType();
...
}
{% endhighlight %}

**Examples Of Reflection**

Use Class.newInstance() to call the default constructor 
{% highlight java %}
Example:
abstract class Foo {
public static Foo create() throws Exception {
String className = System.getProperty(
“foo.implementation.class”,
“com.example.myproject.FooImpl”);
Class c = Class.forName(className);
return (Foo)c.newInstance();
}
abstract void op1(...);
abstract void op2(...);
}
...
Foo obj = Foo.create();
obj.op1(...);{% endhighlight %}

This technique is used in CORBA:
- CORBA is an RPC (remote procedure call) standard
- A system property specifies which implementation of CORBA is used
- A CORBA application can be written in a portable way
- Specify the implementation you want to use via a system property
(pass –D<name>=<value> command-line option to the Java 
interpreter)
Same technique is used for J2EE:

A plug-in architecture
Use a properties file to store a mapping for
plugin name ‡ class name 
- Many tools support plugins: Ant, Maven, Eclipse, …

{% highlight xml %}
Example Ant build file
<?xml version=“1.0”?>
<project name=“example build file” ...>
<property name=“src.dir” value=“...”/>
<property name=“build.dir” value=“...”/>
<property name=“lib.dir” value=“...”/>
<target name=“do-everything”>
<mkdir dir=“...”/>
<mkdir dir=“...”/>
<javac srcdir=“...” destdir=“...” excludes=“...”/>
<jar jarfile=“...” basedir=“...” excludes=“...”/>
<foo .../>
</target>
<taskdef name=“foo” classname=“com.example.tools.Foo”/>
</project>
{% endhighlight %}



Spring (cont’)
n Spring uses reflection to create an object for each bean
- The object’s type is specified by the class attribute
n By default, the object is created with its default constructor
- You can use constructor-arg elements (nested inside bean) to use 
a non-default constructor
n After an object is constructed, each property is examined
- Spring uses reflection to invoke obj.setXxx(value)
- Where Xxx is the capitalized name of property xxx
- Spring uses reflection to determine the type of the parameter passed to 
obj.setXxx()
- Spring can support primitive types and common Collection types
- The ref attribute refers to another bean identified by its id

Example:
Below is an extract from a Spring configuration file:
{% highlight xml %}
<?xml version=“1.0”?>
<beans ...>
<bean id=“employee1”
class=“com.example.xyz.Employee”>
<property name=“firstName” value=“John”/>
<property name=“lastName” value=“Smith”/>
<property name=“manager” ref=“manager”/>
</bean>
<bean id=“manager”
class=“com.example.xyz.Employee”>
<property name=“firstName” value=“John”/>
<property name=“lastName” value=“Smith”/>
<property name=“manager” ref=“manager”/>
</bean>
...
</beans>
{% endhighlight %}

Reflection is a very powerful concept and it’s of little use in normal programming but it’s the backbone for most of the Java, J2EE frameworks. Frameworks that use reflection are:
JUnit - JUnit 3 uses reflection to find methods whose names start with “test”  and  JUnit 4 test methods are identified by an annotation
Spring – dependency injection, read more at Spring Dependency Injection
Tomcat web container to forward the request to correct module by parsing their web.xml files and request URI.
Eclipse auto completion of method names
Struts
Hibernate

The list is endless and they all use reflection because all these frameworks have no knowledge and access of user defined classes, interfaces, their methods etc.

**Drawbacks Of Reflection**
We should not use reflection in normal programming where we already have access to the classes and interfaces because of following drawbacks.
Poor Performance – Since reflection resolve the types dynamically, it involves processing like scanning the classpath to find the class to load, causing slow performance.
Security Restrictions – Reflection requires runtime permissions that might not be available for system running under security manager. This can cause you application to fail at runtime because of security manager.
Security Issues – Using reflection we can access part of code that we are not supposed to access, for example we can access private fields of a class and change it’s value. This can be a serious security threat and cause your application to behave abnormally.
High Maintenance – Reflection code is hard to understand and debug, also any issues with the code can’t be found at compile time because the classes might not be available, making it less flexible and hard to maintain.


