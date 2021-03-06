---
layout: post
title: "Simple Factory"
description: "Simple Factory"
category: Design Patterns
tags: [Java, Creational Design Pattern]
published: true
author: aakash01
---
{% include JB/setup %}

### Simple Factory

> * Define a class that encapsulates object creation.
> * Creates an object without exposing the instantiation logic to the client.
> * Refers the newly created object using a common interface.

![simple factory]({{http://aakash01.github.io}}/assets/images/design_patterns/simplefactory.png)

The Simple Factory isn't actually a design pattern; It's more of a programming idiom.

Simple Factory can be defined as a static method and is called static factory. By defining as static method we don't need to 
instantiate an object to make use of create method. But the drawback is that we can't subclass and change the behaviour of the 
create method;

**Example**


![simple factory example]({{http://aakash01.github.io}}/assets/images/design_patterns/simplefactory_example.PNG )

-   -   -

#### Code (Java)
``` java
public class SimplePizzaFactory {
   public Pizza createPizza(String type) {
      Pizza pizza  = null;
      switch(type){
      case "cheese" :
         pizza = new CheesePizza();
         break;
      case "pepperoni" :
         pizza = new PepperoniPizza();
         break;
      case "veggie" :
         pizza = new VeggiePizza();
         break;
      }
      return pizza;
   }
}
```
``` java
public class PizzaStore {
   SimplePizzaFactory factory;
   
   public PizzaStore(SimplePizzaFactory factory){
      this.factory = factory;
   }
   
   public Pizza orderPizza(String type){
      Pizza pizza;
      
      pizza = factory.createPizza(type);
      
      pizza.prepare();
      pizza.bake();
      pizza.box();
      
      return pizza;
   }
}
```
-----------------------------