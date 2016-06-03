---
layout: post
title: "Creational Design Patterns"
description: "Creational Design Patterns"
category: Programming
tags: [Java]
published: true
author: aakash01
---
{% include JB/setup %}

### Simple Factory

> * Define a class that encapsulates object creation.
> * Creates an object without exposing the instantiation logic to the client.
> * Refers the newly created object using a common interface.

![simple factory]({{http://aakash01.github.io}}/assets/images/simplefactory.png)

The Simple Factory isn't actually a design pattern; It's more of a programming idiom.

Simple Factory can be defined as a static method and is called static factory. By defining as static method we don't need to 
instantiate an object to make use of create method. But the drawback is that we can't subclass and change the behaviour of the 
create method;

**Example**


![simple factory example]({{http://aakash01.github.io}}/assets/images/simplefactory_example.jpg ){:height="480px" width="950px"}

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
-----------------------------

### Factory Method Pattern

> **The Factory Method Pattern** defines an interface for creating an object, but lets subclasses decide which class to instantiate. 
Factory Method lets class defer instantiation to subclasses.

**Factory Method relies on Inheritence:** object creation is delegated to subclasses which implement the factory method to create objects. 

![Diagram]({{http://aakash01.github.io}}/assets/images/factorymethod_pattern.jpg){:height="400px" width="900px"}

> A factory method handles object creation and encapsulates it in a subclass. This decouples the client code in the superclass from the object creation code in subclass.

![abstract Product factoryMethod(String type)]({{http://aakash01.github.io}}/assets/images/factory_method.png)

----------------------------

#### Advantages : 
1. Factory method eliminate the need to bind application-specific classes into the code. The code only deals with the product interface, 
that way we are decoupling the implementation of the product from its use, therefore it can work with any user-defined ConcreteProduct classes.
2. It gives subclasses a hook for providing extended version of the object. 
3. Connects parallel class hierarchies : It encapsulates product knowledge into each creator. 

-----------------------------
    
####   Example

![Example]({{http://aakash01.github.io}}/assets/images/factorymethod_pattern_example.jpg)


``` java
public abstract class PizzaStore {
   public Pizza orderPizza(String type){
      Pizza pizza;
      
      pizza = createPizza(type);
      
      pizza.prepare();
      pizza.bake();
      pizza.box();
      
      return pizza;
   }
   
   protected abstract Pizza createPizza(String type);
}
```
``` java
public class NYStylePizzaStore extends PizzaStore {
   Pizza createPizza(String type){
      switch(type){
      case "cheese":
         return new NYStyleCheesePizza();
      case "veggie":
         return new NYStyleVeggiePizza();
      default:
         return null;
      }
   }
}
```

------------------------------------------


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



