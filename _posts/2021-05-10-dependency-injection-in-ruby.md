---
title: OOP Dependency Injection with a car example
date: 2021-05-02
layout: post
permalink: /dependency-injection-ruby-car/
tags: 
    - ruby
---

I’ve been listening to more of [Sandi Metz presentations](https://www.youtube.com/watch?v=YtROlyWWhV0) and [reviewing notes](https://github.com/serodriguez68/poodr-notes) from her book [Practical Object Oriented Designs](https://www.amazon.com/Practical-Object-Oriented-Design-Agile-Primer/dp/0134456475/ref=sr_1_1?dchild=1&keywords=poodr&qid=1620758320&sr=8-1).

I reflected back on my own code I wrote in Ruby on Rails a few years ago. I wasn’t shy about making ‘fat models’. I created a God class that did everything and was hard to test.

Here’s how I’d go about breaking up class that has too many responsibilities into several objects that do what they need to do.

Let’s go through an example of a `Car` object in Ruby.

```ruby
class Car
  attr_reader :running

  def initialize
    @running = false
  end

  def engine_on
    @running = true
  end

  def engine_off
    @running = false
  end
end
```

We can instantiate a car object `car = Car.new`. When we get inside a car, we stick our key in and we turn on the engine, right?

We add two methods called `engine_on` and `engine_off`.

Engine doesn’t belong in a car.

Notice that we added two methods that start with a noun engine and end with a behavior on / off. These methods are inside a `Car` class. Why the heck is Car responsible for telling an engine how to turn on?

When you start writing methods inside a class with nouns (engine) that don’t belong to that class (Car), that’s an object that’s screaming to be created.

What can an `Engine` do? It can be turned on and off. Let’s create a simple Engine Object.

```ruby
class Engine
  def initialize
    @on = false
  end
  
  def on
    @on = true
  end
  
  def off
    @on = false
  end
end
```

How do we bring the Engine back into the Car? One way of doing that is to instantiate it from the Car object.

Note that we can now change the method names from `engine_on` (noun + behavior) to a full behavior `turn_on`. Same goes for `turn_off`.

```ruby
class Car
  def initialize
    @engine = Engine.new # Instantiate the engine from here.
  end

  def turn_on
    @engine.on
  end

  def turn_off
    @engine.on
  end
end
```

Above is an improvement from before but the Car still knows too much about the Engine. It knows an `Engine` class exists and that you can instantiate a new engine object from it.

A `Car` should be modular. When you buy a car and it is built, you can specify what engine or color you’d prefer, right? A car doesn’t make that decision itself. You do.

To make car a bit more loosely coupled, we can use Dependency Injection to bring in the Engine like this:

```ruby
class Car
  # Dependency Injection
  def initialize(engine: Engine.new)
    @engine = engine 
  end

  def turn_on
    @engine.on
  end

  def turn_off
    @engine.on
  end
end
```

Let’s instantiate a car object and turn it on.

```ruby
car = Car.new(engine: Engine.new)
# or the car by default injects Engine.new

car = Car.new
# <Car:0x00007fde7d070e50 @engine=#<Engine:0x00007fde7d070d60 @on=false>>

car.turn_on #true
car
# #<Car:0x00007fde7d070e50 @engine=#<Engine:0x00007fde7d070d60 @on=true>>
# Note that the engine turned on! @on=true
```

Okay, so where’s the advantage? Cars have different engines. A Diesel engine needs to be warmed up in the winter before it can start while a gas engine doesn’t care.

# Antipattern Example

Let’s look at an inefficient way to take into account a diesel and a gasoline engine and turn the car on.

```ruby
class Car
  def initialize(engine = Engine.new)
    @engine = engine
  end

  def turn_on
    # The start up is different based on the type of engine you're using.
    if @engine.kind == 'Diesel'
      @engine.warm_up
      @engine.on
    else
      @engine.on
    end
  end
end
```

Notice that the `turn_on` method just became complicated with a conditional. The car now has to know how to start an engine properly. It’s doing too much. An engine should be able to take a message and know how to start itself.

Also take a look at what we had to do to the engine class:

```ruby
class Engine
  attr_reader :kind
  def initialize(kind: 'Gasoline')
    @on = false
    # We had to add two extra instance variable to keep track of
    # the kind of engine it is and whether it's warm.
    # Warm is only relevant for a Diesel engine, not a gasoline one.
    @warm = false
    @kind = kind
  end

  def on
    @on = true
  end

  def off
    @on = false
  end

  # warm_up method is only relevant to the Diesel Engine.
  # It's not needed at all for a gasoline engine. We're polluting this class.
  def warm_up
    @warm = true
  end
end
```

# Refactor

Don’t make the Car object thing about how each engine should start. The car object should only worry about sending a `on` message to an engine and the engine should do whatever it has to do to start itself.

The hint we should have taken was that there are two types of engines. Two nouns. Two engine objects? Yes! A `GasolineEngine` and a `DieselEngine`.

```ruby
class GasolineEngine
  def initialize
    @on = false
  end

  def on
    @on = true
  end
end

class DieselEngine
  def initialize
    @on = false
    @warm = false
  end

  def on
    warm_up
    @on = true
  end

  private
  def warm_up
    @warm = true
  end
end
```

Notice that the `DieselEngine` is a bit more complex. It has a `@warm` instance variable to track whether it has been warmed up. A `GasolineEngine` does not need that and doesn’t have it.

The important part is that both Engine classes can respond to `on`. They both have a `on` method. However, both have a different procedure to follow to turn on. That’s key. Let each do it’s own thing. Don’t allow the `Car` object to micromanage and tell and the engine how to turn on.

Here’s how the `Car` class looks like:

```ruby
class Car
  def initialize(engine: GasolineEngine.new)
    @engine = engine
  end

  def turn_on
    @engine.on
  end

  def turn_off
    @engine.on
  end
end
```

Let’s instantiate.

```ruby
car = Car.new
car 
#<Car:0x00007fbfa882bda0 @engine=#<GasolineEngine:0x00007fbfa882bd78 @on=false>>
# A Gasoline Engine is passed in by default.  @on = false.
car.turn_on # Car sends a message to the engine to turn on.
car
#<Car:0x00007fbfa882bda0 @engine=#<GasolineEngine:0x00007fbfa882bd78 @on=true>>
# It turned on without the car worrying about how to do it.

# Let's try it with a Diesel Engine.
car = Car.new(engine: DieselEngine.new)
car
#<Car:0x00007fbfa70dbdf8 @engine=#<DieselEngine:0x00007fbfa70dbe48 @on=false, @warm=false>>
car.turn_on
car
#<Car:0x00007fbfa70dbdf8 @engine=#<DieselEngine:0x00007fbfa70dbe48 @on=true, @warm=true>>
# DieselEngine took care of warming itself up and starting the car!
```

The Car object only has to command an engine to turn on. We managed to get rid of the conditional complexity we had before. The code is easy to read and each object does it’s own job.

That’s the power of dependency injection and breaking a God class into different objects.
