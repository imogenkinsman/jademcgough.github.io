---
layout: post
title: Kernel Conversion Methods
date: 2014-07-17 23:43:12
---

There have been a number of great posts (such as [this one](http://devblog.avdi.org/2012/05/07/a-ruby-conversion-idiom/) from Avdi Grimm) about the handy conversion methods in Ruby's Kernel module. I couldn't find an in-depth discussion about these, and my standard ruby documentation sources didn't fully explain their quirks, so hopefully this helps someone who's curious in the future.

## Kernel#Array
Calls arg.to_ary, then arg.to_a in that order. If neither are defined on the object, this simply returns [arg].

## Kernel#String
Calls arg.to_s. This is guaranteed to work in practical terms, since Object#to_s is defined (unless you plan on trying this on a BasicObject object).

(Note: #to_s should not be confused with #to_str, which not synonymous and is a topic for another discussion.)

## Kernel#Hash
Calls arg.to_hash. Unlike Kernel#String, this isn't defined on Object and Kernel#Hash will raise a TypeError if #to_hash is not defined on the provided object.

## A Note on Return Values
By using Kernel methods, you are guaranteed to either get back the requested object type or raise a TypeError. If you try to cheat and define a to_* method that returns the wrong type, your evil plans will be foiled. Ruby checks the return type and will raise a TypeError if it doesn't match.

{% highlight ruby %}
class A
  def to_a
    "An Array"
  end
end

> a = A.new
> Array(a)
TypeError: can't convert A to Array (A#to_a gives String)
{% endhighlight %}