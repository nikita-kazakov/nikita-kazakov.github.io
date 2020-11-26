---
title: How Object Oriented Design Works
date: 2020-10-10
layout: post
permalink: /how-object-oriented-design-works/
tags: 
    - Ruby
---

It took me a while to understand how objects in Object Oriented languages work. Once it clicked, I needed to share what made it click.

Let's break down what an object is in object oriented programming. An object could be anything but let's ground ourselves with something simple.

Let's use Jim --- a person --- as the object.

Like any other human, Jim stores information in his brain.

I'm going to grossly over-simplify the brain into two parts. We're not learning biology here. This simplified model will help you understand how objects store data and communicate with other objects.

{% include image_center_caption.html 
    caption = "Jim's brain and the part of it that stores data about Jim has a circle around it."
    image = "/assets/images/2020/how-object-oriented-works/01a.jpg"
    alt = "Jim's brain and the part of it that stores data about Jim has a circle around it."
%}

I won't know the data inside Jim's brain unless he chooses to share it with me.

All the data in his brain is **private to him**. This is similar to when a cop apprehends a suspect and tells him "you have the right to remain silent".

All data inside the circle is isolated, or using a fancier programming vocabulary word, it is **ENCAPSULATED**. It is isolated from all things outside the circle.

I can't telepathically read Jim's mind.

If I ask "What's your name?" --- his brain needs to understand my request (message) and have a way to respond to it.

The second part of our over-simplified brain understands language. It is able to respond to questions. Unlike us, it has direct access to Jim's data circle.

{% include image_center_caption.html 
    caption = "The cortex circle has direct access to Jim's data and can respond to requests from us."
    image = "/assets/images/2020/how-object-oriented-works/01.jpg"
    alt = "The cortex circle has direct access to Jim's data and can respond to requests from us."
%}

Using this analogy we'll understand how objects store data and how they understand messages and respond to them.

# Asking a question

Here's what happens when you ask Jim his name:

  1. Jim receives the question
  2. If the cortex circle understands the question, it can ask the data circle for Jim&#8217;s name.
  3. Data circle sends Jim's name to the cortex.
  4. The cortex responds with 'Jim'.
  
{% include image_center_caption.html 
    caption = "The four things that happen when asking Jim his name."
    image = "/assets/images/2020/how-object-oriented-works/03.jpg"
    alt = "The four things that happen when asking Jim his name."
%}

The cortex is the middle man between you and Jim's data. You can't get to Jim's data directly without first going through the cortex circle.

Let's redraw this as two concentric circles. The inner circle is the data circle and the outer circle contains knowledge about your questions. The cortex is like an ambassador between you and Jim's data circle.

{% include image_center_caption.html 
    caption = "The outer cortex circle (ambassador) and the inner data circle."
    image = "/assets/images/2020/how-object-oriented-works/04.jpg"
    alt = "The outer cortex circle (ambassador) and the inner data circle."
%}

What happens if you ask a question that Jim's cortex can't understand? You ask his name in Russian but he doesn't speak Russian.

{% include image_center_caption.html 
    caption = "The outside circle (the ambassador) does not understand the question you asked and cannot grab his name from Jim's data circle"
    image = "/assets/images/2020/how-object-oriented-works/04.jpg"
    alt = "The outside circle (the ambassador) does not understand the question you asked and cannot grab his name from Jim's data circle"
%}

Even though Jim's age is available in his data circle, the cortex circle cannot understand the question you just asked. You don't get a response back.

Using the above analogy, we covered that objects data is encapsulated within the object (stays private) unless it is exposed by the cortex (getters). By asking Jim's name, we sent a **message** to Jim.

Let's use Ruby to model what we discussed above.

# Jim as a Ruby Object

In Object Oriented programming, we often create objects --- known as instantiating --- from a class. A class is like a factory template.

Jim is a person. To get Jim, we'll instantiate Jim from a Person class (factory).

Let's write an empty Person class.

```ruby
class Person
end
```

The Person class will hold two pieces of data. The Person's name and age. We'll use a special Ruby initialize method to build those two parameters.
```ruby
class Person
  def initialize(name, age)
  end
end
```

Now, we can instantiate a Jim object out of a Person class and store it in `jim` local variable. If you inspect it, you'll notice it isn't holding any data.

```ruby
jim = Person.new("Jim", 20)
jim.inspect # => <Person:0x00007fed7ac3a2c0>
```

That's because we forgot to store the parameters we pass into the Person class as instance variables. Let's do with a `@name` and `@age` instance variables.
```ruby
class Person
  def initialize(name, age)
    @name = name
    @age = age
  end
end
```

```ruby
jim = Person.new("Jim", 20)
jim.inspect # => "#<Person:0x00007fb8428be7a8 @name=\"Jim\", @age=20>"
```

The Jim object is now storing a name and age. Those instance variables are the data circle we talked about in our analogy. Remember, we don't have direct access to that data. Let's try accessing Jim's name and see what happens.

```ruby
jim.name # => undefined method `name'
```

His name and age are private data that is encapsulated to Jim's object. We need a cortex, the ambassador to understand our request for Jim's name and give us his name. In Ruby, this ambassador is called a method. Specifically, it's a getter method because it's *getting* a piece encapsulated data from Jim.

```ruby
class Person
  def initialize(name, age)
    @name = name
    @age = age
  end
  
  # Add a getter method to get Jim's name
  def name
    @name
  end
end
```

```ruby
jim.name # => "Jim"
```

It worked! We wrote a getter method, which is an ambassador between us and Jim's data. By writing `jim.name`, we send a `name` message to Jim. The name method recognizes that message and returns the value of the `@name` instance variable to us.

The name of the method could be whatever you want it to be. You could have said:

```ruby
def what_are_you_called
  @name
end 

jim.what_are_you_called # => "Jim"
```

You could also return anything from a method including:

```ruby
def name
  "My name is " + @name
end

jim.name # => "My name is Jim"
```

We can ask for Jim's name but we still can't ask for his age. Without looking ahead, go ahead and write a getter method that send a message to Jim to get his age.

```ruby
class Person
  def initialize(name, age)
    @name = name
    @age = age
  end

  # Getter method to get Jim's name
  def name
    @name
  end
  
  # Getter method to get Jim's age
  def age
    @age
  end
end

jim.name # => "Jim"
jim.age # => 20
```

Methods (ambassadors) that are defined within a class have direct access to data (instance variables) of that class.

Write a method that asks Jim to tell us his name and age in one sentence.

```ruby
def name_and_age
  "My name is " + @name + " and my age is" + @age
end 

jim.name_and_age # => "My name is Jim and my age is 20"
```

## Setter Methods
What if we wanted to change Jim's age to something else?

```ruby
jim.age = 30 # => NoMethodError: undefined method `age='
```

We get an error. Jim doesn't know what to do with that. Jim doesn't have an ambassador to change that instance variable. 

We can fix this by writing a **setter** method. Why a setter? Because it *sets* a new value.

```ruby
class Person
  def initialize(name, age)
    @name = name
    @age = age
  end
  
  # setter method to SET Jim's age.
  def age=(num)
    @age = num
  end
end

jim.age = 30 # No errors
```

Pop Quiz Hotshot --- If you ask for Jim's age `jim.age` you'll get an error. Why?

It's because we erased the getter method that gave us Jim's age. Let's put it back. I wanted to demonstrate that setter methods don't need getter methods to work.

```ruby
class Person
  def initialize(name, age)
    @name = name
    @age = age
  end

  # setter method to SET Jim's age.
  def age=(num)
    @age = num
  end

  # Getter method to get Jim's name
  def name
    @name
  end
end

jim.age = 30
jim.age # => 30
```

# attr_reader, attr_writer, attr_accessor
Ruby was made for developer happiness. And let's face it, developers are lazy and in our case, it's a virtue. In Ruby you'll seldom getter and setter methods explicitly written as we have above.

There's a shortcut to having Ruby write them for you.

- `attr_reader` writes a getter method.
- `attr_writer` writes a setter method.
- `attr_accessor` writes a getter AND setter method.

Let's open the Person class again and add a getter method for name using `attr_reader`.

```ruby
class Person
  attr_reader :name
  
  def initialize(name, age)
    @name = name
    @age = age
  end
end

jim.name # => "Jim"
```

Notice we used `:name`. That's a symbol. We're naming it based off `@name` instance variables. Just remove the `@` and add the `:`.

You can add multiple getters on one line.

```ruby
attr_reader :name, :age
```

Let's allow other objects to ask Jim for his name and age but only allow other objects to set Jim's age.

```ruby
attr_reader :name, :age
attr_writer :age
```

Let's say Jim is a very open person, we can add getters and setters to his name and age like this:

```ruby
attr_accessor :name, :age
```

There's nothing magical about these `attr_` methods. Ruby writes the same exact getter and setter methods we wrote manually above.

```ruby
# This below
attr_accessor :name

# is the same as writing:
def name
  @name
end
```

```ruby
# This below
attr_writer :age

# is the same as writing:
def age=(num)
  @age = num
end
```

```ruby
# This below
attr_accessor :age

# Writes both the getter and setter methods for age.
def age
  @age
end

def age=(num)
  @age = num
end
```

# Instantiating Objects from Classes

Since the Person class is a factory, we can create (instantiate) other people with other names and ages.

```ruby
class Person
  # Add getter and setter methods to both name and age.
  attr_writer :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end
end

# Create 3 different Person objects.
jim = Person.new("Jim", 20)
sally = Peron.new("Sally", 40)
bob = Person.new("Bob", 70)

jim.name # => "Jim"
sally.age # => 40

# Let's change Sally's age
sally.age = 100

jim.age # => 20
sally.age # => 100
bob.age # => 70

jim.age + sally.age + bob.age # => 190
```

Notice how each object tracks it's own internal data. That's because in object oriented languages, objects have data (instance variables) and behavior (methods).


# Mapping an Object

An object in object oriented programming works very similarly as Jim did above. An object can be anything. Let&#8217;s say we have a cash register object. Just like Jim, an object that you create can have properties that you can specify. In this example, we created a cash amount of $200 as one property of this cash register. We can write as many as we want.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-22-1024x536.png" alt="" class="wp-image-6962" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-22-1024x536.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-22-300x157.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-22-768x402.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-22.png 1188w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

When we ask an object for something and an object responds, that&#8217;s better understood as sending a message.

If I send a message to the cash register asking for the cash amount, what should happen?

Remember, we don&#8217;t have direct access to the cash data. To us the object properties are hidden. They are private to the object. They are encapsulated.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-23.png" alt="" class="wp-image-6963" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-23.png 638w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-23-300x285.png 300w" sizes="(max-width: 638px) 100vw, 638px" /> </figure> 

The middle man circle that envelops the dark data circle is empty. The cash register object receives the **cash_amount?** message, it doesn&#8217;t know what to do with it.

Objects are not as smart as humans when making sense of what is asked of them. That&#8217;s where YOU come in. You have to specifically write the the messages that objects will understand and how they will respond to them.

In programming these messages are called **methods**.

Let&#8217;s say you write a **cash_sum?** method in the cash register object that will grab the cash value ($200) directly from the data circle and return it. You can now send a **cash_sum?** message to the cash register and it will know how to respond to you.<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-24.png" alt="" class="wp-image-6965" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-24.png 634w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-24-300x287.png 300w" sizes="(max-width: 634px) 100vw, 634px" /> </figure> 

## Methods

How do you know which messages (methods) an object should understand? Ask yourself, what should your object be able to do?

A cash register should be able to store cash (data) and you should be able to check the value of it, deposit money, and withdraw money from the register.

With that implemented, here&#8217;s how the cash register object looks like:<figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-26.png" alt="" class="wp-image-6967" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-26.png 922w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-26-300x285.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-26-768x730.png 768w" sizes="(max-width: 922px) 100vw, 922px" /> </figure> 

As a person trying to use this object, all you see is that this object understanding three messages `withdraw`, `cash_sum?`, and `deposit`. You have no idea what data the object is holding in the data circle. 

## Sending Messages

To send a message to an object, you first specify the object followed by a dot and then the message.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">cash_register.cash_sum?    #200
</pre>

Let&#8217;s say you want to deposit or withdraw money into / from the cash register. The next question is how much? You can pass the amount as an argument with the message like this.

<pre class="EnlighterJSRAW" data-enlighter-language="generic" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">cash_register.deposit(25)
cash_register.withdraw(50)</pre>

As an outsider passing a message to the cash register, you don&#8217;t need to worry about **HOW** it handles what you tell it to do. The cash register will do that internally. Again, that&#8217;s the idea of encapsulation. You trust the object to handle the messages you send to it without you meddling in them.

## Examples of Objects

Let&#8217;s take a look at how other objects might look like. Notice that with the TV remote object, I cannot send a message to it asking for it&#8217;s color or width. It won&#8217;t understand those messages as it doesn&#8217;t have them defined in the outer circle.

<pre class="EnlighterJSRAW" data-enlighter-language="ruby" data-enlighter-theme="" data-enlighter-highlight="" data-enlighter-linenumbers="" data-enlighter-lineoffset="" data-enlighter-title="" data-enlighter-group="">tv.color #error message. No method found.</pre><figure class="wp-block-image size-large">

<img src="https://nikitakazakov.com/wp-content/uploads/2020/02/image-27-1024x537.png" alt="" class="wp-image-6973" srcset="https://nikitakazakov.com/wp-content/uploads/2020/02/image-27-1024x537.png 1024w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-27-300x157.png 300w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-27-768x402.png 768w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-27-1536x805.png 1536w, https://nikitakazakov.com/wp-content/uploads/2020/02/image-27.png 1664w" sizes="(max-width: 1024px) 100vw, 1024px" /> </figure> 

## Takeaways

  * When sending a message to an object, an object will always respond back. The response may be an error but there will always be a response.

link to understanding everything is an object post.