---
layout: post
title: "Facade Pattern"
description: "Facade Pattern -- Class,Object Structural"
category: Programming
tags: [Java, Structural Patterns]
published: true
author: aakash01
---
{% include JB/setup %}

``` 
The Facade Pattern provides a unified interface to a set of interfaces in a subsystem. 
Facade defines a higher level interface that makes the subsystem easier to use.
```


![Facade Pattern]({{http://aakash01.github.io}}/assets/images/facade_pattern.png )

1. Use Facade to simplify and unify a large interface or complex set of interfaces. 
2. It decouples a client from a complex subsystem. 
3. It shields client from subsystem components, thereby reducing the number of objects that client has to deal with and making the subsystem easier for use. 
4. Promotes weak coupling between the subsystem and client. 
5. It defines a higher level interface without hiding the lower-level functionality. So the applications can use the subsystem classes if they have to.

It promotes `Principle of least knowledge` or `law of demeter`.

**Principle of least knowledge** --- *Talk only to your immediate friends*
