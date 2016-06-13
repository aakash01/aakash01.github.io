---
layout: post
title: "The Adapter Pattern"
description: "Adapter Pattern -- Class,Object Structural"
category: Design Patterns
tags: [Java, Structural Patterns]
published: true
author: aakash01
---
{% include JB/setup %}

### Converts one interface to another.

>   **The Adapter Pattern** converts the interface of a class to another interface the client expects. Adapter lets classes work together that couldn't otherwise because of incompatible interfaces.
>   Also known as **Wrapper**.

![adapter pattern]({{http://aakash01.github.io}}/assets/images/adapter_pattern.jpg )

1   The client makes a request to the adapter by calling a method on it using the target interface.

2   The adapter translate that request into one or more calls on the adaptee using the adaptee interface.

3   The client receives the results of the call and never knows there is an adapter doing the translation. 


*   When we need to use an existing class and its interface is not the one we need, then use adapter.
*   Adapter Changes an interface into one a client needs.


There are two forms of adapter pattern

### Object Adapter
**Object Adapter relies on object composition**

![Class Diagram]({{http://aakash01.github.io}}/assets/images/object_adapter.jpg )

It lets a single Adapter work with many Adaptees, the Adaptee itself and all of its subclasses. But it is harder to override Adaptee behaviour because 
it will require subclassing Adaptee and making Adapter refer to the subclass instead of Adaptee itself.


### Class Adapter

**A Class Adapter uses multiple inheritance to adapt one interface to another**.

![Class Diagram]({{http://aakash01.github.io}}/assets/images/class_adapter.jpg )

It adapts Adaptee to Target by committing to a concrete Adapter class. As a consequence, a class adapter won't work when we want to adapt a class and all its subclasses.
But it lets Adapter override some of Adaptee's functionality as it is a subclass of Adaptee.

--------------------------------------

#### Example :

``` java
public interface Enumeration {
   
   public boolean hasMoreElements();
   
   public Object nextElement();
   
}
```
``` java
public interface iterator {
   
   public boolean hasNext();
   
   public Object next();
   
   public void remove();
}
```
``` java
public class EnumerationAdapter implements iterator {
   private Enumeration enumObj;
   
   public EnumerationAdapter(Enumeration enumObj){
      this.enumObj = enumObj;
   }

   @java.lang.Override
   public boolean hasNext() {
      return enumObj.hasMoreElements();
   }

   @java.lang.Override
   public Object next() {
      return enumObj.nextElement();
   }

   @java.lang.Override
   public void remove() {
      throw new UnsupportedOperationException();
   }
}
```

#### Examples in JAVA API.

`java.io.InputStreamReader(InputStream)` --- translate a byte stream into character stream.

`java.io.OutputStreamWriter(OutputStream)` --- translate a character stream into byte stream.