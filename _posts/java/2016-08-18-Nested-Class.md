---
layout: post
title: "Nested Class"
description: "Nested Class in java"
category: Java
tags: [Java]
published: true
author: aakash01
---
{% include JB/setup %}

>   Nested Class

A nested class is a class defined within another class. A nested class should exists only to serve enclosing class. 

We have 4 types of nested classes. 

1. Static Member

2. Non-Static Member

3. Anonymous class

4. Local class


**Static Member Class**

A Static Member class is a static member of its enclosing class and obeys the same accessibility rules as other static members. 

``` java
class outer {
   static class Inner {
      void test(){
         System.out.println("Test Function");
      }
   }
   
   public static void main(){
      Inner inner = new Inner();
      inner.test();
   }
}
```

Instance of static class can exists without outer class instance. 


**Member Class**

A Member class is a non static member of enclosing class. It can not exists without outer class instance ie. Each instance of non-static member class is associated
with an instance of enclosing class and can be accessed via Outer.this . 

Eg:

``` java
class MyMap<E> extends AbstractSet<E> {
   public Iterator<E> getIterator(){
      return new MyIterator();
   }
   
   class MyIterator implements Iterator<E> {
      
   }
}
```
``` java
Outer outer = new Outer();
Inner inner = outer.new Inner();
```

Defining an inner class is expensive. 


**Local Class**

A local class is defined inside a code block or method. They have the same scope as local variable. They can't be public, private or protected but they can be final. 


Eg: 

``` java
class Outer {
   public static void main(String[] args) {
      class Local{
         void test(){
            System.out.println("Test function");
         }
      }
      Local local = new Local();
      local.test();
   }
}
```

**Anonymous Class**

Anonymous Inner Class is a class which doesn't have a name to reference and initialized at the same place where it is created. 

``` java
class Outer {
   public static void main(String[] args) {
      Thread anonymous = new Thread() {
         @Override
         public void run(){
            System.out.println("Anonymous thread");
         }
      };
      
      anonymous.start();
   }
}
```


