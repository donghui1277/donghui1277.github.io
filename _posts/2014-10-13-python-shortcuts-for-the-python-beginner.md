---
layout: post
title: "<i class='icon-retweet'></i> Python Shortcuts for the Python Beginner"
description: 
headline: 
modified: 2014-10-13
category: retweet
tags: [python]
image: 
  feature: 
comments: true
mathjax: 
---

This post retweet from [maxburstein](http://maxburstein.com/blog/python-shortcuts-for-the-python-beginner/).

The following are just a collection of some useful shortcuts and tools I've found in Python over the years. Hopefully you find them helpful.

##Swapping Variables##

{% highlight python linenos %}
x = 6
y = 5
 
x, y = y, x
 
print x
>>> 5
print y
>>> 6
{% endhighlight %}

##Inline if Statement##

{% highlight python linenos %}
print "Hello" if True else "World"
>>> Hello
{% endhighlight %}

##Concatenations##

The last one is a pretty cool way to combine objects of two different types.

{% highlight python linenos %}
nfc = ["Packers", "49ers"]
afc = ["Ravens", "Patriots"]
print nfc + afc
>>> ['Packers', '49ers', 'Ravens', 'Patriots']
 
print str(1) + " world"
>>> 1 world
 
print `1` + " world"
>>> 1 world
 
print 1, "world"
>>> 1 world
print nfc, 1
>>> ['Packers', '49ers'] 1
{% endhighlight %}

##Number Tricks##

{% highlight python linenos %}
#Floor Division (rounds down)
print 5.0//2
>>> 2
 
#2 raised to the 5th power
print 2**5
>> 32
{% endhighlight %}

Be careful with division and floating point numbers.

{% highlight python linenos %}
print .3/.1
>>> 2.9999999999999996
 
print .3//.1
>>> 2.0
{% endhighlight %}

##Numerical Comparison##

This is a pretty cool shortcut that I haven't seen in too many languages.

{% highlight python linenos %}
x = 2
 
if 3 > x > 1:
    print x
>>> 2
 
if 1 < x > 0:
    print x
>>> 2
{% endhighlight %}

##Iterate Through Two Lists at the Same Time##

{% highlight python linenos %}
nfc = ["Packers", "49ers"]
afc = ["Ravens", "Patriots"]
 
for teama, teamb in zip(nfc, afc):
    print teama + " vs. " + teamb
 
>>> Packers vs. Ravens
>>> 49ers vs. Patriots
{% endhighlight %}

##Iterate Through List With an Index##

{% highlight python linenos %}
teams = ["Packers", "49ers", "Ravens", "Patriots"]
for index, team in enumerate(teams):
    print index, team
 
>>> 0 Packers
>>> 1 49ers
>>> 2 Ravens
>>> 3 Patriots
{% endhighlight %}

##List Comprehension##

With a list comprehension we can turn this:

{% highlight python linenos %}
numbers = [1,2,3,4,5,6]
even = []
for number in numbers:
    if number%2 == 0:
        even.append(number)
{% endhighlight %}

Into this:

{% highlight python linenos %}
numbers = [1,2,3,4,5,6]
even = [number for number in numbers if number%2 == 0]
{% endhighlight %}

Pretty sweet huh?

##Dictionary Comprehension##

Similar to the list comprehension we can also do a dictionary comprehension like this:

{% highlight python linenos %}
teams = ["Packers", "49ers", "Ravens", "Patriots"]
print {key: value for value, key in enumerate(teams)}
>>> {'49ers': 1, 'Ravens': 2, 'Patriots': 3, 'Packers': 0}
{% endhighlight %}

Initialize List Values

{% highlight python linenos %}
items = [0]*3
print items
>>> [0,0,0]
{% endhighlight %}

##Converting a List to a String##

{% highlight python linenos %}
teams = ["Packers", "49ers", "Ravens", "Patriots"]
print ", ".join(teams)
>>> 'Packers, 49ers, Ravens, Patriots'
{% endhighlight %}

##Get Item From Dictionary##

I'll admit that try/except code doesn't look the prettiest. Here's a simple way to fix that with dictionaries. This will try to find the key in the dictionary and if it can't be found it will set the variable to the second parameter.

Instead of:

{% highlight python linenos %}
data = {'user': 1, 'name': 'Max', 'three': 4}
try:
    is_admin = data['admin']
except KeyError:
    is_admin = False
{% endhighlight %}

Do this:

{% highlight python linenos %}
data = {'user': 1, 'name': 'Max', 'three': 4}
is_admin = data.get('admin', False)
{% endhighlight %}

##Taking a Subset of a List##

Sometimes you only want to run code over a portion of a list. Here are a few ways you can get the subset of a list.

{% highlight python linenos %}
x = [1,2,3,4,5,6]
 
#First 3 
print x[:3]
>>> [1,2,3]
 
#Middle 4
print x[1:5]
>>> [2,3,4,5]
 
#Last 3
print x[-3:]
>>> [4,5,6]
 
#Odd numbers
print x[::2]
>>> [1,3,5]
 
#Even numbers
print x[1::2]
>>> [2,4,6]
{% endhighlight %}

##FizzBuzz in 60 Characters##

A while back Jeff Atwood popularized a simple programming exercise called [FizzBuzz](http://www.codinghorror.com/blog/2007/02/why-cant-programmers-program.html). Here is the excerpt on the problem:

Write a program that prints the numbers from 1 to 100. But for multiples of three print "Fizz" instead of the number and for the multiples of five print "Buzz". For numbers which are multiples of both three and five print "FizzBuzz".
Here's a short, fun way to solve the problem.

{% highlight python linenos %}
for x in range(1,101):print"Fizz"[x%3*4:]+"Buzz"[x%5*4:]or x
{% endhighlight %}

##Collections##

In addition to python's built in datatypes they also include a few extra for special use cases in the [collections](http://docs.python.org/2/library/collections.html) module. I find the Counter to be quite useful on occasion. Some of you may even find it useful if you're participating in this year's [Facebook HackerCup](https://www.facebook.com/hackercup).

{% highlight python linenos %}
from collections import Counter
 
print Counter("hello")
>>> Counter({'l': 2, 'h': 1, 'e': 1, 'o': 1})
{% endhighlight %}

##Itertools##

Along with the collections library python also has a library called [itertools](http://docs.python.org/2/library/itertools.html) which has really cool efficient solutions to problems. One is finding all combinations. This will tell us all the different ways the teams can play each other.
{% highlight python linenos %}
from itertools import combinations
 
teams = ["Packers", "49ers", "Ravens", "Patriots"]
for game in combinations(teams, 2):
    print game
 
>>> ('Packers', '49ers')
>>> ('Packers', 'Ravens')
>>> ('Packers', 'Patriots')
>>> ('49ers', 'Ravens')
>>> ('49ers', 'Patriots')
>>> ('Ravens', 'Patriots')
{% endhighlight %}

##False == True##

This is more of a fun one than a useful technique. In python True and False are basically just global variables. Thus:
{% highlight python linenos %}
False = True
if False:
    print "Hello"
else:
    print "World"
 
>>> Hello
{% endhighlight %}

If you've got any other cool tips/tricks leave them in the comments below. Thanks for reading!
