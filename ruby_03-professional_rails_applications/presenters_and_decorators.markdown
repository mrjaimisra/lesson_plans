---
title: Decorators & Presenters
length: 90
tags: presenters, decorators, rails, refactoring, mvc
---

## Learning Goals

* Understand the decorator pattern
* Practice rewriting helpers using a Draper decorator
* Understand the theory and purpose of a presenter object
* Practice creating a presenter to collect and wrap data

## Structure

* 30 - Lecture: Intro to Decorators
* 30 - Tutorial: Experimenting with Draper
* 15 - Lecture: Intro to Presenters
* 15 - Code: Creating a Dashboard Presenter

## Lecture: Intro to Decorators

### Decorator Basics

* Decorators are a Software Pattern concerned with
* Most implementations of the Decorator pattern are built around
  "wrapping" and "delegation"
* Decorators are a good demonstration of
  the [Open/Closed Principle](https://en.wikipedia.org/wiki/Open/closed_principle) --
  we are able to add functionality to the wrapped object without
  modifying it directly
* Decorators in ruby also exploit ruby's use of duck typing -- since
  they delegate unknown methods to the internal/wrapped object, they
  effectively preserve the same interface and can be used
  interchangeably.

__Workshop -- Building Your Own Decorator__

Can you implement a simple decorator object which has the following
behaviors:

* Accepts another object (call it model, for example) as its
  initialization argument
* Defines its own methods which can be accessed just like a normal
  object
* Additionally will "pass through" any methods that are called on it
  to the underlying object

An example usage API might look something like this:

```
MyDecorator.new(MyModel.new).model_only_method
=> "called a model method"

MyDecorator.new(MyModel.new).decorator_only_method
=> "called a decorator method"
```

### Decorators as View Models

* __Q:__ What is the standard tool in rails for abstracting view-layer
  responsibilities?
* __Q:__ What are some downsides to this approach?
* __Q:__ What might a more object-oriented approach to view-layer
  interactions look like?

### Decorator Pattern - Popular Libraries

There are quite a few libraries out there that implement this pattern,
including one particularly popular one by some guy named Casimir.

Let's take a look at some Draper basics.

* [Draper Docs](https://github.com/drapergem/draper)

## Tutorial: Experimenting with Draper

[Work through this tutorial](http://tutorials.jumpstartlab.com/topics/decorators.html)
using Decorators to extract some view logic from Blogger.
If you get done with the core tutorial, then try out the bit at the end about
creating XML and JSON from your decorator.

## Lecture: Intro to Presenters

### Presenter Basics


Consider these 4 rules from Sandy Metz for practicing good Rails
hygiene:

1. Your class can be no longer than 100 lines of code.
2. Your methods can be no longer than five lines of code.
3. You can pass no more than four parameters and you can't just make it one big hash.
4. When a call comes into your Rails controller, you can only instantiate one
   object to do whatever it is that needs to be done. And your view can only know about one instance variable.

The first 3 are probably familiar to us at this point (even if we
grumble about them), but what about that last one?

We've certainly seen Rails controllers and views that utilized more
than one object. So how can we reconcile the need to get things done
with this outline for code cleanliness?

Presenters are a technique for solving this problem.

* Similar to Decorators, Presenters are a pattern for abstracting
  complexity in our view/presentation layer
* Decorator -- Adds functionality (often view-related) to a single
  object (or possibly collection of objects)
* Presenter -- Combines functionality across _multiple objects_
  into a single interface
* A presenter is just another domain object -- one that represents
  a larger abstraction across multiple objects
* In more complicated scenarios, Presenters and Decorators can be
  used in conjunction
* No library needed -- just POROs!
* Example: creating a `Dashboard` presenter

## Code: Creating a Dashboard

Go back to your Blogger project a presenter for the Dashboard such
that the **only** instance variable in `views/dashboard/show.html.erb` is
`@dashboard`.

If you get that working, try creating a `DashboardDecorator`. What logic can
you pull out of the view template into the decorator?
