---
layout: post
title: "Decorator Pattern"
description: "Decorator Pattern -- Object Structural"
category: Design Patterns
tags: [Java, Structural Patterns]
published: true
author: aakash01
---
{% include JB/setup %}

``` 
The Decorator Pattern attaches additional responsibilities to an object dynamically. 
Decorator provide a flexible alternative to subclassing for extending functionality. 
```
Also known as **Wrapper**. It involves a set of decorator classes that are used to wrap concrete components. 

![Decorator Pattern -- Class Diagram]({{http://aakash01.github.io}}/assets/images/decorator_pattern.jpg )

### Key Points
*   Decorators have the same supertype as the objects they decorate. 
*   One or more decorators can be used to decorate an object. 
*   As the decorator has the same supertype as the object it decorates, we can pass around the decorated object in place of original object .
*   **The Decorator adds its own behaviour before and/or after delegating to the object it decorates to do the rest of the job. **
*   It uses composition. 
*   Objects can be dynamically decorated at runtime. 


``` java
public abstract class Beverage {
   String description;

   public String getDescription() {
      return description;
   }
   
   public abstract double cost();
}

public abstract class CondimentDecorator extends Beverage {
   public abstract String getDescription();
}
```
``` java
public class Espresso extends Beverage {

   public Espresso() {
      description = "Espresso";
   }

   @Override
   public double cost() {
      return 0;
   }
}
```
``` java
public class Mocha extends CondimentDecorator {
   Beverage beverage;

   public Mocha(Beverage beverage) {
      this.beverage = beverage;
   }

   @Override
   public double cost() {
      return 0.50 + beverage.cost();
   }

   @Override
   public String getDescription() {
      return beverage.getDescription() + "Mocha.";
   }
}

// USAGE
Beverage espresso = new Espresso();
Beverage espressoWithMocha = new Mocha(espresso);
Beverage espressoWithDoubleMocha = new Mocha(espressoWithMocha);

```

#### Examples in JAVA API.

java.io package is largely based on decorator. 

**BufferedInputStream** and **LineNumberInputStream** both extend **FilterInputStream**, which acts as the abstract decorator class. 


``` java
public class LowerCaseInputStream extends FilterInputStream {
   public LowerCaseInputStream(InputStream in) {
      super(in);
   }
   
   public int read() throws IOException {
      int c = super.read();
      return (c== -1 ? c : Character.toLowerCase((char)c));
   }
}
   
//Example
InputStream in = new LowerCaseInputStream(new BufferedInputStream(new FileInputStream("input.txt")));
```


