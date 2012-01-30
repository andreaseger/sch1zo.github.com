---
layout: post
title: "JS playground 1: mustache and ICanHaz.js"
date: 2012-01-29 16:53
comments: true
categories: 
- javascript
- mustache
- icanhaz
---
Over the last few days I started to play around with javascript and other front-end related stuff.

The first thing I wanted to try and use was [mustache](http://mustache.github.com/).
So first I needed a backendt to serve the templates and the dynamic data. Of course I used Ruby 
and Sinatra for this. For the views the server had to render I also used Mustache - that's the nice 
thing about Mustache you can use it everywhere.

Mustache as it is is really nice, after you understood how it will use partials and how it goes through 
the data you get in my optinion much nicher source template als in someting like erb. Also you don't 
depend on some magic like when using haml or slim. And of course the split between data and template 
really helps to structure your code.

So now to the interesting part the client side. After a few very simple tests on how to use mustache.js 
I accounted the problem on how to get the templates to the client without having to write them directly 
into the javascript file.
I looked around and discoverd [ICanHaz.js](http://icanhazjs.com/), which is a nice wrapper around 
mustache and tries to solve the template issue.
There are two ways to register a template for ICanHaz, the first one is to write them into the html like this:

``` html
<script id="group" type="text/html">
  //the template
</script>
```

But to use this you have to write all your templates into the html source, which I didn't liked.

The other way is to get the templates via JS as JSON from the server and just add them to ICanHaz:

``` javascript
$.getJSON('/myserver/templates.json', function (templates) {
    $.each(templates, function (template) {
        ich.addTemplate(template.name, template.template);
    });
});
```

Thats really clean and your have your templates seperate from the rest of the javascript and html.
