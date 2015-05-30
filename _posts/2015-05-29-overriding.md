---
layout: post
title: Overriding
---

Reimplementing the inherited method from the parent class in the child class is called __Overriding in Java__.

There are certain __rules for overriding__, in the below code we will point out all of the rules:

{% highlight java linenos %}

class Animal {

    private void drink() {
        System.out.println("Animal Drink");
    }

    protected void walk() {
        System.out.println("Animal Walk");
    }

    public void eat() {
        System.out.println("Animal Eat");
    }

    public void run() {
        System.out.println("Animal Run");
    }

    public void sleep() throws IOException {
        System.out.println("Animal Sleep");
    }

    public Animal getAnimal() {
        return new Animal();
    }
}

class Horse extends Animal {

    private void drink() {  // Not a method override as drink()
                            // wasn't inherited by Horse class
        System.out.println("Horse Drink");
    }

    private void eat() {    // You can't use a more
                            // restrictive access modifier
                            // (gives you a compiler error)
        System.out.println("Horse Eat");
    }

    public void walk() {    // Valid method override as you can use less restrictive
                            // access modifier in the overriding method
        System.out.println("Horse Walk");

    }

    public void run(int n) {    // Not a method override (argument list differs)
                                // but rather a method overload of run() in Animal
        System.out.println("Horse Run");
    }

    public Horse getAnimal() {  // Valid method override as return type must
                                // be the same as, or a subtype of, the return type
                                // declared in the original overridden method in the superclass
        return new Horse();
    }

    public void eat() throws Exception {    // Not a method override as the overridden method doesn't
                                            // throw any checked exceptions while overriding method does
                                            // (gives a compiler error)
        System.out.println("Horse Eat");
    }

    public void sleep() throws FileSystemException {    // Valid method override as FileSystemException
                                                        // is a subclass of IOException
        System.out.println("Horse Sleep");
    }

    public void sleep() throws Exception {  // Not a method override as Exception is neither
                                            // same as nor a subclass of IOException
                                            // (gives a compiler error)
        System.out.println("Horse Sleep");
    }
}

public class Overriding {

    public static void main (String [] args) {
        Animal a = new Animal();
        Animal b = new Horse();  // Animal ref, but a Horse object
        Horse h = new Horse();

        a.eat();    // Runs the Animal version of eat()
        b.eat();    // Runs the Horse version of eat()
                    // (Concept called Dynamic method invocation)

    }
}

{% endhighlight %}

Some more rules which may be obvious:

* You cannot override a method marked `final`.
* You cannot override a method marked `static`.
* If a method can't be inherited, you cannot override it. As said earlier,
overriding implies that you're reimplementing a method you inherited.