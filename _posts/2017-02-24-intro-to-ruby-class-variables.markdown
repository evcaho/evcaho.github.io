---
title: "A simple introduction to class variables in Ruby"
layout: post
date: 2017-02-24 22:44
headerImage: false
tag:
- ruby
- beginner
star: false
category: blog
author: eviech
description: A simple introduction to class variables in Ruby
---

One thing that confused me for a while was the difference between instance variables and class variables. Instance variables are used across an entire class, right? So shouldn't they be called class variables?

Well, no. NOT AT ALL. 

For starters: classes can contain both class and instance variables. Class variables apply to an entire class, whereas instance variables are called on one *instance* of a class (like `Soda.new()`). 

Every time I call `new` to create a new `Soda` object, my instance variable data can change. But if I create three `Soda` objects, my class variables will remain the same for all of them. 

An instance variable looks like this: `@name = ` and class variables are `@@total_drinks = `. In my `Soda` class I use both: 

```ruby
class Soda
  @@total_drinks = 0

  def initialize(name, sweetener, ranking)
    @name = name
    @sweetener = sweetener
    @ranking = ranking
    @@total_drinks += 1
  end

  def ranking
    puts "#{@name} ranking: #{@ranking} of #{@@total_drinks}"
  end

end
```

Every time I create a new instance of `Soda`, the class variable ``@@total_drinks`` changes.

```ruby
soda1 =  Soda.new("Shasta", "high-fructose corn syrup", 1)
```

If I created two instances of `Soda.new()`, the `@@total_drink` value would become 2 in both instances. 

```ruby
soda1 =  Soda.new("Shasta", "high-fructose corn syrup", 1)
soda2 = Soda.new("Jones", "cane sugar", 2)
soda1.ranking #Shasta ranking: 1 of 2
soda2.ranking #Jones ranking: 2 of 2
```

## Using class variables for inheritance 

Class variables are also useful because they can be inherited from other classes.

Now, if I created a class that inherited characteristics from `Soda`, like `DietSoda` (since it's a type of soda), I can access the ``@@total_drinks`` variable because it's a class variable.  I want diet sodas should be counted in my total drinks number. 

So if I call `new` to create a new `DietSoda` object, ``@@total_drinks`` value would add up to three (`soda1`, `soda2`, and now `dietsoda1`) 

```ruby
class DietSoda < Soda
end

diet1 = DietSoda.new("Diet Pepsi", "aspartame", "3")
diet1.ranking #Diet Pepsi ranking: 3 of 3
```


### So, should you use a class variable for that? 

Most Ruby projects are going to use instance variables a heck of a lot more than class variables. 

Inheritance is best used when your inheriting class or object is a *kind* of the inherited class (like diet soda for soda, or men's pants for clothing) that would contain similar characteristics. 

That said, classes should be as self-contained as possiblem so introducing class variables, with their own pieces of data, can get unwieldy and end up acting as global variables (bad news). So class variables [understandably](http://stackoverflow.com/questions/10594444/class-variables-in-ruby) [get](http://archive.oreilly.com/pub/post/nubygems_dont_use_class_variab_1.html) [a](http://archive.oreilly.com/pub/a/ruby/excerpts/ruby-best-practices/worst-practices.html) [bad](https://railsless.blogspot.com/2013/09/class-variables-on-class-in-ruby.html) rap and are just too hard to control. 

[Here's a resource](https://www.sitepoint.com/class-variables-a-ruby-gotcha/) that discusses when to actually use class variables, and [this resource discusses composition](https://learnrubythehardway.org/book/ex44.html), which can be used in place of inheritance. 

Happy using class variables responsibly! 