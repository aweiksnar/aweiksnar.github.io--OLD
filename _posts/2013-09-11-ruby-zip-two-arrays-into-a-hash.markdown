---
layout: post
title:  "Ruby: Zip Two Arrays Into A Hash"
date:   2013-09-11 23:55:31
categories: ruby syntax array zip hash
published: true
---

Here is a neat trick for turning two arrays (of equivalent length) into a hash.

But first, a small syntax shortcut that I will use for creating the arrays from ranges, courtesy of the splat operator.

Include the splat operator inside of an array created with the bracket syntax, and the expanded version will be returned:

{% highlight ruby %}
[*1..10]  # => [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
[*"A".."J"]  #=> ["A", "B", "C", "D", "E", "F", "G", "H", "I", "J"]
{% endhighlight %}

Since the splat operator can be used to collect values, in this context it collects the values of the range and places them inside the array.

Let's say that we wanted to merge the above arrays into a hash so that the letters are keys to the numerical values. This can be accomplished with the [.zip](http://www.ruby-doc.org/core-2.0.0/Array.html#method-i-zip) method, which can pair the two arrays of equivalent length when used with the [Hash[]](http://www.ruby-doc.org/core-2.0.0/Hash.html#method-c-5B-5D) method.

{% highlight ruby %}
Hash[[*"A".."J"].zip [*1..10]]
#=> {"A"=>1, "B"=>2, "C"=>3, "D"=>4, "E"=>5, "F"=>6, "G"=>7, "H"=>8, "I"=>9, "J"=>10}
{% endhighlight %}

If the lengths do not match ruby will give precedence to the length of the keys array. If if is shorter than the length of the values array it will stop creating pairs when the hash size reaches that length:

{% highlight ruby %}
Hash[[*"A".."C"].zip [*1..10]]  #=> {"A"=>1, "B"=>2, "C"=>3}
{% endhighlight %}

If it is longer ruby will assign nil values to the superfluous keys:

{% highlight ruby %}
Hash[[*"A".."J"].zip [*1..3]]
#=> {"A"=>1, "B"=>2, "C"=>3, "D"=>nil, "E"=>nil, "F"=>nil, "G"=>nil, "H"=>nil, "I"=>nil, "J"=>nil}
{% endhighlight %}
