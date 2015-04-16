---
layout: post
title: "Dive into Java   Part 2"
description: ""
category: 
tags: []
---
{% include JB/setup %}

> What is an Abstract Class? 

Abstract classes in java are those classes which can not be instantiated. They serve as base for child classes. 

**Abstract Methods**
Abstract Methods are methods which do not have any implementation. A class containing an abstract method should be declared abstract. Methods declared abstract are compulsory to be overridden by child class. 
Eg: 
{% highlight java %}
public abstract class AbstractClass {
    public abstract void abstractMethod();
    public void nonAbstractMethod(){
    //Do Something
}

}
{% endhighlight %}

An Abstract class can contain abstract as well as non abstract methods.

**So what is the purpose of abstract class?**

Abstract classes are used to provide abstraction.

<blockquote class="blockquote-reverse">
<p class="text-muted">
In computer science, abstraction is the process by which data and programs are defined with a representation similar in form to its meaning (semantics), while hiding away the implementation details.
<footer>Source : WikiPedia</footer>

<ol>
<li> <kbd>Data abstraction</kbd><br/>
Data abstraction is the way to create complex data types and exposing only meaningful operations to interact with data type, where as hiding all the implementation details from outside works.
		</li>
<li> <kbd>Control abstraction</kbd><br/>
		Control abstraction is the process of identifying repetitive statements and expose them as a fucntion.
		</li>
		</ol>

</p>
</blockquote>
The purpose of abstract class is to function as base classes which can be extended by subclasses to create a full implementation. For Eg.
We have a media player which requires 3 actions

1. Start Media Player
2. Play Something
3. Stop Media Player

We can implement this in abstract class like 

{% highlight java %}
public abstract MediaPlayer {

    public void process() {
        startPlayer();
        play();
        stopPlayer();
    }

    public void startPlayer() {
    	System.out.println("startPlayer");
    	//Generic Implemntation
        //implementation directly in abstract superclass
        //Child class can also override this
    }

    public abstract void play(); // implemented by subclasses

    public void stopPlayer() {

    	System.out.println("stopPlayer")
        //Generic Implemntation
        //implementation directly in abstract superclass
        //Child class can also override this
    }
}
{% endhighlight %}

Here the Play method is abstract and will be override by child class. When the process() method of the subclass is called, the full process is executed, including the action() method of the subclass.
Eg:

{% highlight java %}
public AVIPlayer extends MediaPlayer {

	@Override
    public void play(){
    	System.out.println("Playing AVI Movie");
    }

}
{% endhighlight %}

{% highlight java %}
MediaPlayer aVIPlayer = new AVIPlayer();

aVIPlayer.process();

//Output
startPlayer
Playing AVI Movie
stopPlayer
{% endhighlight %}



