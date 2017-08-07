---
title: "Single quotes vs. double quotes in Ruby"
layout: post
date: 2017-01-13 22:44
headerImage: false
tag:
- ruby
- beginner
star: true
category: blog
author: eviech
description: 
---

In Ruby, strings can be encased in either single or double quotes. Most beginning Ruby books have you begin Ruby using single quotes, but switch to double quotes upon introducing string interpolation. It's much easier to write out:

```ruby
num_people = 4 + 5
"there are #{num_people} people going to the fair."
```
than

```ruby
num_people = 4 + 5
'There are ' + num_people + ' people going to the fair.'
```

But which one is better? And does it even matter, especially when you're starting out?

### Speed vs. Speed

There are a few reasons why single quotes get touted as "better": they're faster to parse, there are less escape sequences (for single quotes and a single backslash). The old rule of thumb was to use single quotes unless using string interpolation. 

Well, single quotes *are* faster ([as this Viget article points out ](https://www.viget.com/articles/just-use-double-quoted-ruby-strings). The reason is that your computer/the lexer is going to spend time scanning the string for `#{}`. But the difference is minute. **Like, statistically insignificant.** 

If you're a relatively new Ruby developer, you probably don't need to worry about speed.

But there's another speed we haven't discussed: **yours**. 

Single quotes require you to ask yourself if you're going to use string interpolation now or down the road. If this changes, editing the code is harder and leaves more room for error. Plus, the single quote escape sequence (`\'`) is going to be used more often than double quotes because we use single quotes a lot more in written language than double (remember apostrophes?). There may be more [escape sequences with double quotes] (https://en.wikibooks.org/wiki/Ruby_Programming/Strings#Double_quotes) but they're used less often.

### Bottom Line

For most projects and most developers, double quotes are far easier to maintain.