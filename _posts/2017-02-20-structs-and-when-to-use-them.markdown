---
title: "Fantastic structs and when to use them"
layout: post
date: 2017-02-24 22:44
headerImage: false
tag:
- ruby
- beginner
star: false
category: blog
author: eviech
description: A simple introduction to structs in Ruby.
---

I'm working my way through Sandi Metz' *Practical Object-Oriented Design in Ruby* because I find myself making the same clumsy design mistakes in my code. In Chapter 2, she makes use of Ruby structs as a way to bundle data together without having to create an entire class. 

Imagine that I wanted to create a Person class with only a few attributes. If I wanted to do that as a struct, I can set it up this way: 

```ruby
Person = Struct.new(:name, :location)
```

Notice that the parameters (name, location) are written similarly to accessors in classes. 

Once I've set up my new `Person` struct, I can create an instance of it, which I'm calling `author`: 

```ruby
author = Person.new("Evie", "Washington")
```

...all without having to create a `Person` class and type out an initialize method or `attr_accessor`s. Pretty neat. 

I can also access the instance's attributes by calling:

```ruby
author.name #Evie
author.location #Washington
``` 

## But why?
Structs can help clean up your code so you don't have to create attr_accessors and an initialize methods for an object that's just a collection of data or attributes.  Here's what `Person` would look like as a class: 

```ruby
class Person
	attr_accessor :name, :location
	def initialize(name, location)
		@name = name
		@location = location
	end
end

person = Person.new("Evie", "Washington")
person.name #Evie
person.location #Washington
```
That same class, setup as a struct, looks like this: 

```ruby
Person = Struct.new(:name, :location)
author = Person.new("Evie", "Washington")
puts author.location #Evie
puts author.name #Washington
```
What's more is that classes can inherit from these structs. 

```ruby
Person = Struct.new(:name, :location)
class Author < Person
end

first_person = Author.new("evie", "wa")
puts first_person.name #evie
```

## Struct pitfalls and proper usage
Sandi Metz' argument for using structs is to help structure data and make your code as clean and clear as possible. So how can they be best used? 

Struct attributes are structured (har har), [whereas you can pass any data into a hash or array](http://culttt.com/2015/04/15/working-with-structs-in-ruby/). They're useful if you know all the attributes of your object. 

And if I miss an attribute in creating a new struct object, it will return nil instead of an error:

```ruby
puts Person.new("Evie") #struct Person name="Evie", location=nil
```

Sometimes this is what you want and sometimes it isn't. 

Structs work best when they're treated **just** as data containers. As Henrik Nyh points out, [inheriting from structs can lead to all sorts of problems](https://thepugautomatic.com/2013/08/struct-inheritance-is-overused/). 

So keep your structs simple and your inheritance miniman. Only you can prevent struct overuse and determine what your data needs. 