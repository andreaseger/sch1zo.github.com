---
layout: post
title: "Octopress for the win"
date: 2012-01-02 05:02
comments: true
categories: 
- meta
- perl
---
New Year, new Blog.

I decided to kill my tumblr and start this octopress blog. At the moment I 
just imported most of the old posts and fixed tags/categories, but I still 
have to check all links and move some images.

And just for the record here are a few of the snippets used to convert the
posts.

``` sh
# download and extract posts in jekyll format
wget https://github.com/stephenmcd/jekyll/blob/master/lib/jekyll/migrators/tumblr.rb
ruby -r './tumblr' -e 'Jekyll::Tumblr.process("http://sch1zo.tumblr.com",format="md")'

# exchange tags for categories
perl -pi -e '$.==4 and s/tags/categories/;close ARGV if eof' *

# add a tumbler tag/category to each post
perl -pi -e '$.==5 and s/^/- tumblr\n/;close ARGV if eof' *
```

yeah I know, Perl WTF!? These snippets just were the first thing google/stackoverflow gave me
after searching for this kind a task, and I didn't want to convert them to Ruby
or anything else.

Unfortunatly I couldn't find a way to write the date into the meta data of the
file. Perhaps I'm just to tired...

Here is what I got(this time in ruby). After failing here I just went ahead ant edited the 19 files
by hand.

``` sh
ruby -pie '$.==4 and $_.sub!(/^/, "date: #{"2011-03-02-here should be the current filename".match(/(\d{4}-\d{2}-\d{2}).*/)[1]}\n")' *
```
