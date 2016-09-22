---
layout: post
title: "Exceptions"
description: "Exceptions"
category: Articles
tags: [Java]
published: true
author: aakash01
---
{% include JB/setup %}


### Java Throwable Hierarchy

![Throwable]({{http://aakash01.github.io}}/assets/images/java/Exceptions.PNG )



**Error** 

Errors are exceptional scenarios which are out of the scope of application and it is not possible  to recover from them. 


**Checked Exceptions**

They are checked at compile time and must be either catched or thrown. Eg: IOException. 



**Unchecked Exceptions**

They are not checked at compile time, also known as RuntimeExceptions. Eg: NullPointerException.


**Try**

Try is used to enclose the code that might throw an exception. It must be followed by catch or finally. 


**Catch**

Catch is used with try to catch an exception. With java7 we can catch multiple exceptions with one catch block. 

Eg: 

``` java
try{
   // IO or SqlException. 
} catch (IOException | SqlException e){
   e.printStackTrace();
}
```

**Finally**

Finally is used with try. The code inside finally is always executed, even on return or an exception. It is used to freeup resources. 



**Throw**

Throw keyword is used to throw an exception. 

``` java 
public void method(){
    throw new RuntimeException();
}
```

**Throws**

Throws is used to propogate an exception from a method. 

``` java
public void someMethod() throws Exception1, Exception2{
}
```

> If an exception is thrown inside both try and finally, then the finally exception will be propogated
and try exception will be suppressed. 

> With Java7 we can use getSuppressed to get suppressed exceptions. 
In case of try-with-resources , suppressed exception will be automatically added otherwise we will have to manually add it. 

``` java
Throwable.getSupressed(); // Returns Throwable[]
Throwable.addSupressed(aThrowable);
```

**Try-With-Resources (Java 7)**

``` java
try(FileInputStream input = new FileInputStream("..");
    BufferedInputStream bis = new BufferedInputStream(input)){
    int data = bis.read();
}
```

After executing try-with-resources, input and bis will close automatically. All the classes implementing **AutoClosable** can be used with try-with-resource. No need to use finally. 

> If an exception is thrown from both try-with-resource block and close method, then the exception of try-with-resource  will be propogated and close exception will be suppressed. This is opposite of try-finally. 


