# Classes Review

## Objectives
* Review and gain a basic understanding of Classes and Objects
* Create simple classes
* Define fields (variables for state) and methods (functions for behavior) in classes  
* Instantiate objects (instances of classes) from classes, using constructors
* Call methods on objects from classes

## Resources
* [Video: Classes and Objects](http://www.youtube.com/watch?v=OHw2t8BaIUg)
* [Video: Methods](http://www.youtube.com/watch?v=-eoNHtILOs4)
* [Video: Getters and Return Values](http://www.youtube.com/watch?v=foX28s2Qw0w)
* [Video: Method Parameters](http://www.youtube.com/watch?v=fXVI4xuvozg)
* [Video: Setters and 'this'](http://www.youtube.com/watch?v=x-gBJ6q3Ufc)
* [Video: Constructors](http://www.youtube.com/watch?v=oSiN1J_G01Q)
* [Video: Static and Final Keywords](http://www.youtube.com/watch?v=yImBET6EO8c)

# Lecture

Ealier in this course, we covered the concept of Object-Oriented Programming. In Java, **objects** are blocks of code, with their own variables and methods, which are created, or **instantiated**, based on a blueprint called a **class**.

Let's look at this class as an example:

```java
public class Apple {
  private boolean isRipe;
  private int seedCount;

}
```

The ```class``` ```Apple``` is a blueprint of sorts - and an object of class Apple is simply an ```instance``` of an Apple. Let's **instantiate** an object of the class ```Apple```:

```java
class Main {
  public static void main(String[] args) {
    Apple apple = new Apple();
  }

}
```

Great! The variable ```apple``` is of the type ```Apple```, and at runtime, will hold a reference to the object in memory of type ```Apple```. We created an object of the class ```Apple``` by calling its **default constructor**.

However, we can't really do much with this object. We have no access to its fields (they are set to **private**), and we haven't assigned any values to these fields. We've created an object, but it is a poorly constructed one.

First, let's 