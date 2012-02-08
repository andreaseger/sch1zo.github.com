---
layout: post
title: "FYI: dynamically define methods in ruby"
date: 2012-02-08 12:17
comments: true
categories: 
- ruby
- fyi
---

to create a method dynamically do something like this:

``` ruby
[:teacher, :group, :course, :room].each do |arg|
  method_name = ("find_by_" + arg.to_s).to_sym
  define_method(method_name) do |params|
    # to stuff here
  end
end
```

if the methods should be class methods modifier it like this

``` ruby
class << self
  [:teacher, :group, :course, :room].each do |arg|
    method_name = ("find_by_" + arg.to_s).to_sym
    define_method(method_name) do |params|
      # to stuff here
    end
  end
end
```
