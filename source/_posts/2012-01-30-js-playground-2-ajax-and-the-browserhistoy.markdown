---
layout: post
title: "JS playground 2: AJAX and the Browserhistoy"
date: 2012-01-30 22:26
comments: true
categories: 
- javascript
- ajax
- browserhistoy
---
So after managing to render my data on the client - see my last post about mustache - I wanted to get the 
browser histoy working again. The problem with single site pages and getting all the data via ajax is that 
normally the browserhistory is useless. Also you can't bookmark stuff or send others a link to exacly the 
site you are seeing.

With HTML5 there is now a clean way of doing exaclty this task. With the Histoy API, nicely explained 
[here](https://developer.mozilla.org/en/DOM/Manipulating_the_browser_history) from mozilla, you can now 
add new items to the browser history. This works more or less like a stack, if you want to add something 
just push a new state to it. If the user then clicks back the last element gets poped from the stack. The 
API also allows you to save some data in each state - besides the URI itself. In addition you can walk 
through the history in javascript, but I didn't play with this.

Fortunatly I don't care for old browsers, so I could just use this as all(?) modern Browsers support the Histroy API.
But as with most of these features every browser does it a little bit different. I normally test apps in Opera, because 
thats my main browser, and I got the history woring pretty fast. So I thought lets see what Chrome does with this and of 
couse it didn't work. I'm not sure if i used the API in a wrong way or if Chrome or Opera does something special here. 
Point is even after fiddling around for a bit it didn't work in both browsers at the same time.

I think it should look somethink like this, but sometimes the popstate event is not the one you would want and you have to use the originalEvent and sometimes not.

``` javascript
$(window).bind("popstate", function(e) {
  var state = e.originalEvent().state
  // do stuff
});

// make a new state
history.pushState(data, title, url);
```

So whats the solution for that kind of problem? Just ask the internet if anybody has written a nice wrapper for this 
which takes care about the different browsers. And suprise, suprise I found [history.js](https://github.com/balupton/History.js/)

Because I already knew how and when to add new states and how to act on a 'back' event, the change to history.js was 
pretty easy. Just had to change some keywords. And it almost immedialety work in all browsers I tested it (opera, chrome, firefox)

``` javascript
History.Adapter.bind(window,'statechange',function(){
  var state = History.getState()
  // do stuff
});

// make a new state
History.pushState(data, title, url)
```

Besides not having to care about browser differences the libary also supports a fallback mode for non HTML5 browsers, 
which is nice if you care about such stuff.
