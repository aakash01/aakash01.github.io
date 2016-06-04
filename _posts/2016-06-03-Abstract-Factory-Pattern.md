---
layout: post
title: "Abstract factory Pattern"
description: "Abstract factory Pattern"
category: Programming
tags: [Java, Creational Design Pattern]
published: true
author: aakash01
---
{% include JB/setup %}

### Abstract Factory Pattern

> **The Abstract Factory Pattern** provides an interface for creating families of related or dependent objects without specifying their concrete classes.

**Abstract Factory relies on Object Composition**: object creation is implemented in methods exposed in the factory interface.


![class diagram]({{http://aakash01.github.io}}/assets/images/abstract_factory.jpg)

It provide an abstract type for creating a family of products. Subclasses of this type define how the product produced. To use the factory, instantiate one instance and pass it 
into some code that is written against the abstract type. Like Factory Method , the client is decoupled from the actual concrete product. 

-----------------------

#### Advantages

1. Isolates concrete classes. 
2. Makes exchanging product families easy. 
3. Promotes consistency among products.

-----------------------

#### Example 


![Example]({{http://aakash01.github.io}}/assets/images/abstract_factory_example.jpg)

``` java
public interface PizzaIngredientFactory {
   public Dough createDough();
   public Sauce createSauce();
   public Cheese createCheese();
   public Veggies[] createVeggies();
}
```
``` java
public class NYPizzaIngredientFactory implements PizzaIngredientFactory {
   public Dough createDough(){
      return new ThinCrustDough();
   }
   public Sauce createSauce(){
      return new MarianaraSauce();
   }
   public Cheese createCheese(){
      return new NYCheese();
   }
   public Veggies[] createVeggies(){
      return {new Garlic(), new Onion(), new Mushroom()};
   }
}
```
``` java
public abstract class Pizza {
   abstract void prepare();
   // some other methods like cut(), bake() etc.
}
```
``` java
public class Cheesepizza extends Pizza{
   PizzaIngredientFactory ingredientFactory;
   
   public Cheesepizza(PizzaIngredientFactory ingredientFactory){
      this.ingredientFactory = ingredientFactory;
   }
   
   void prepare(){
      dough = ingredientFactory.createDough();
      sauce = ingredientFactory.createSauce();
      cheese = ingredientFactory.createCheese();
   }
}
```



