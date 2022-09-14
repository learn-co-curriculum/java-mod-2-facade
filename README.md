# Facade

## Learning Goals

- Explain the facade pattern
- Use the pattern in Java

## The Facade Pattern

A **facade** is a structural design pattern that hides complexity behind a
simple interface. 

We use the facade pattern when there is complex functionality that we want to
simplify so that it's easier for client classes to use. It abstracts the
complexity of the functionality by tucking it away behind an interface.

Highlights of the facade pattern include:

- Abstraction to simplify a complex system.
- A facade does not add logic of its own - it's just a simple interface to
  existing functionality.
- Internal workings of the facade are not exposed to client systems.

Think of an online store. What we see is a user interface that makes it easy
for us to put products in a virtual shopping cart and then check out. What we
don't see is everything that goes on behind the scenes: the actual placing of
the order to the supplier, the payment gateway, and how taxes are calculated. We
can think of the user interface of an online store as a facade to all the
services happening behind the scenes once we click on the button to check out.

## Implementation

Let's consider our transportation example from the Factory lesson and expand on
it. Say we want to book a ride - whether that be by car, boat, or plane -
through a ride-share. We will still have our `Vehicle` interface with the
implementations of a `Car`, `Boat`, and `Plane`. But we'll add two methods
called `reserve()` and `board()` to be implemented by each of the concrete
classes as well.

We will then create a facade class to hide the implementation details of getting
a ride-share by one of our vehicles. Consider the following updated diagram:

![Ride Share Facade ](https://curriculum-content.s3.amazonaws.com/java-mod-2/facade/Facade-UML.png)

We'll start updating our `Vehicle` interface and its implementations to include
the two new methods:

```java
package com.flatiron.transportation;

public interface Vehicle {
    void travel();
    void reserve();
    void board();
}
```

```java
package com.flatiron.transportation;

public class Car implements Vehicle {
    
    @Override
    public void travel() {
        System.out.println("Traveling by car!");
    }

    @Override
    public void reserve() {
      System.out.println("A car has been reserved for you!");
    }

    @Override
    public void board() {
      System.out.println("Your car has arrived!");
    }
  
}
```

```java
package com.flatiron.transportation;

public class Boat implements Vehicle {

    @Override
    public void travel() {
        System.out.println("Traveling by boat!");
    }

    @Override
    public void reserve() {
      System.out.println("Your boat trip has been reserved!");
    }

    @Override
    public void board() {
      System.out.println("Ahoy! Please embark.");
    }
  
}
```

```java
package com.flatiron.transportation;

public class Plane implements Vehicle {

    @Override
    public void travel() {
        System.out.println("Traveling by plane!");
    }

    @Override
    public void reserve() {
      System.out.println("Your airplane ride has been reserved!");
    }

    @Override
    public void board() {
      System.out.println("Passengers at gate E10 may now board.");
    }
  
}
```

Now let's implement our facade and also make use of the `TransportationFactory`
class we created in the last lesson!

```java
package com.flatiron.transportation;

public class RideShare {
    Vehicle car;
    Vehicle boat;
    Vehicle plane;
    
    RideShare() {
        car = TransportationFactory.getVehicle("CAR");
        boat = TransportationFactory.getVehicle("BOAT");
        plane = TransportationFactory.getVehicle("PLANE");
    }
    
    public void rideCar() {
        car.reserve();
        car.board();
        car.travel();
    }

    public void rideBoat() {
      boat.reserve();
      boat.board();
      boat.travel();
    }

    public void ridePlane() {
      plane.reserve();
      plane.board();
      plane.travel();
      
    }
}
```

As we can see above, the `RideShare` class acts as a facade in that it hides
the implementation details of how we would ride in a car, boat, or plane. This
is a very simple example of a facade design pattern. Imagine how useful this
might be for a more complicated system, like starting and stopping a car that
has to talk to several other components just to turn the ignition on or off.

Now that we have our facade implemented, let's go ahead and test it with a
driver class:

```java
package com.flatiron.transportation;

public class RideShareDriver {
    
    public static main(String[] args) {
        RideShare rideShare = new RideShare();
        
        rideShare.rideCar();
        rideShare.rideBoat();
        rideShare.ridePlane();
        
    }
}
```

If we run the driver class above, we can verify the output looks like this:

```plaintext
A car has been reserved for you!
Your car has arrived!
Traveling by car!
Your boat trip has been reserved!
Ahoy! Please embark.
Traveling by boat!
Your airplane ride has been reserved!
Passengers at gate E10 may now board.
Traveling by plane!
```
