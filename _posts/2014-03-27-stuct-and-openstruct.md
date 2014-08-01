---
layout: post
title: Struct and OpenStruct
date: 2014-03-27 14:40:00
---

Let's talk about two Ruby classes that many newer Rubyists may not be aware of.

## Struct

If you're familiar with structs in the C programming language, Ruby's Struct is very similar - a fast and simple way to encapsulate data.

Here's a simple Ruby class without any defined methods:

{% highlight ruby %}
class Cat
  attr_accessor :color, :age

  def initialize(color, age)
    {{"@"}}color = color
    {{"@"}}age = age
  end
end

kuruneko = Cat.new("black", 16)
{% endhighlight %}

And here's the same class written using Struct:
{% highlight ruby %}
Cat = Struct.new(:color, :age)

kuruneko = Cat.new("black", 16)
{% endhighlight %}

As you can guess, attribute readers/writers are implicitly created by Struct definitions. You'll occasionally see structs written like so:
{% highlight ruby %}
class Cat < Struct.new(:color, :age)
end
{% endhighlight %}

If you see that, find the person who wrote it and shout "BAD! BAD PROGRAMMER!" at them until you feel satisfied. Struct.new returns a new class that interits from Struct, so this adds an unnecessary layer of inheritance. Also, if this gets run twice for whatever reason, you'll get a ```superclass mismatch error```. This happens because you just tried to have Cat inherit from two different classes, since Struct.new creates a unique class object when it executes.

You can even define methods in a struct, though at this point it's probably better just to use a more traditional class declaration.
{% highlight ruby %}
Cat = Struct.new(:color, :age) do
  def meow
    "Meow!"
  end
end
{% endhighlight %}

## OpenStruct

OpenStruct is basically a supercharged struct. Unlike Struct, which requires you to define its attributes when it's created, OpenStruct allows you to arbitrarily create new attributes at will.


{% highlight ruby %}
require 'ostruct'

cat = OpenStruct.new
cat.name = "Mittens"

puts cat.name  # => "Mittens"
{% endhighlight %}

This actually works just like how you'd imagine - an OpenStruct is just a cheap Hash wrapper, perfect for storing key/value pairs. You can even initialize it by passing in a Hash:

{% highlight ruby %}
require 'ostruct'
cat = OpenStruct.new(name: "Mittens")
{% endhighlight %}

So, when would you actually use an OpenStruct? OpenStruct plays really well with Ruby's emphasis on [duck-typing](http://en.wikipedia.org/wiki/Duck_typing). You can think of it as a way to make a dummy object that will respond however you want it to.

In [Avdi Grimm's talk on Confident Coding](https://www.youtube.com/watch?v=T8J0j2xJFgQ), he recommends using it as a way of creating default responses for an object that could be nil.

{% highlight ruby %}
def sayName(args = nil)
  args ||= OpenStruct.new(greeting: "My name is", name: "Jade")
  "#{args.greeting} #{args.name}"
end

sayName # => "My name is Jade"
{% endhighlight %}

And that's Struct and OpenStruct!