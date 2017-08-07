---
title: "How to read Ruby documentation"
layout: post
date: 2017-04-01 22:44
headerImage: false
tag:
- ruby
- beginner
star: true
category: blog
author: eviech
description: Beginners use tutorials while experienced programmers read and refer to documentation. But how do you do that, exactly? This post explains the anatomy of a Ruby doc to help expand your understanding of Ruby.
---


Trying to go from being a beginner to an intermediate programmer can seem like running toward a constantly moving finish line. Tutorials are great, but they can only take you through a set use case, and you still might not understand what's going on under the hood. 

One thing I've noticed: beginners use tutorials while experienced programmers read and refer to documentation. If you're going to move past being a beginner, you need to become comfortable with docs. 

I thought it would be interesting to devote an article entirely to the Ruby docs. I want to clear up misconceptions about using docs, how to understand them, and how to use them more effectively. 

## When should you use the documentation?

The documentation is only useful when you have a question about how a specific class, method or module works. 

For example, you might want to "remove whitespace around a string." You might do a google search and find a Stack Overflow post that references `String#strip`.

Now you're ready to use the Ruby documentation. Head over to [ruby-doc.org](http://ruby-doc.org ) and search for `String#strip`.

Why the extra step? Why not just use Stack Overflow? Stack Overflow works as an introduction to a concept, but the questions are usually too specific. Plus, the answer could be too complicated or use that specific class, method, or module differently than you intend to. It might work for you now, but not the next time you need to use it. 

**Use StackOverflow as a jumping-off point to get to Ruby docs rather than the answer unto itself.**

## Anatomy of a doc

**Nobody expects you to read the Ruby documentation like you would read a book.** Instead, you should use it like a dictionary. 

For example, I may know I need to use the `String#index` method to find the position of a character in a string. So I'll go to the docs looking for **three** pieces of information:

1. **Arguments:** What type of arguments does the method expect?
2. **Return Value:** What type of object does it return?
3. **Operation:** What does the method actually do?

Here's a [link](https://ruby-doc.org/core-2.2.0/String.html#method-i-index) to the documentation for the `String#index` method. I've screenshotted it for your convenience. 

![String#index documentation](/images/2017/02/string_index_documentation.png)

Now lets look at each section in turn.


### Method signatures


At the top of the method's documentation, you'll see this:

```
index(substring [, offset]) → fixnum or nil
```

This is what's called a **"method signature."** It lists the arguments and return values for one form of the method. 

Ruby method signatures follow the pattern:

```
method_name(required_argument [, optional_argument]) → return_types 
```

So far we can deduce the following about `String#index`:

* It has one required argument: a string 
* It has one optional argument: an offset
* It returns either a number or nil. 

If you've been paying attention you may have noticed that the documentation for `String#index` actually has *two* method signatures. This is very common, and the description that follows applies to both method signatures. 

```
index(regexp [, offset]) → fixnum or nil
```

Note that the only difference between the two signatures is the first argument. In the first method signature it was a string. In the second one it's a regular expression i.e. a [regexp](https://ruby-doc.org/core-2.2.0/Regexp.html). 

Now, if you were to ask me about `String#index` I could tell you: "It requires one argument, either a string or a regular expression. There's an optional second argument. It returns either a number or nil."


### The Description

Knowing the method signature is great, but so far we've only seen half of the picture. We know its inputs and outputs but we don't know what it does. 

And if we're being honest, we don't really know what some of the inputs are. For example, I'm not 100% sure what the `offset` argument does. 

These details are usually cleared up in the description:

> Returns the index of the first occurrence of the given substring or pattern (regexp) in str. Returns nil if not found. If the second parameter is present, it specifies the position in the string to begin the search.

It's all clear now! I would attempt to summarize this for you but the summary would be longer than the original text. After all, this a relatively short description. `String#index` is a pretty straightforward method. 

Many method descriptions are more complex. They can seem overwhelming. However if you look closely you will find that most of them follow an if-then structure:

* "If passed a single index, returns a substring of one character at that index." 
* "If pattern is a String, then its contents are used as the delimiter when splitting str."
* "If the increment generates a “carry,” the character to the left of it is incremented."

Once you understand this pattern, it's much easier to skim over the statements and see if any of them apply to your particular use case. 

### Examples

Many of Ruby's methods come with usage examples. While they're often quite helpful it's good to keep in mind that they're only intended to illustrate how to use the method. They're not necessarily suitable to be copy-pasted directly into your production code. 

Use the examples and the descriptions as a way to understand the concept while using the signature as a guide to use and syntax.

## Bottom line

I hope this post helped make sense of how to approach RubyDocs to help you move from tutorials to documentation. Once you know how to approach RubyDocs, your understanding of applying your Ruby knowledge will grow. 