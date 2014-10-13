---
layout: post
title: "Law and/&amp;&amp; Order"
date: 2014-10-13 15:20:55 -0400
comments: true
categories: "Flatiron School"
---

Something that affects nearly every line of code you write, but tends not to receive too much attention is <strong>precedence</strong>, or the order in which operators are evaluated. Maybe that's because it's a somewhat cut and dry subject. What I mean by that is, once you know or reference this...

<a href="http://ruby-doc.org/core-2.1.3/doc/syntax/precedence_rdoc.html">Ruby's Table of Precedence</a>

...you're kind of all set.

But that doesn't mean moments won't arise when your code isn't working the way you'd like and precedence ends up being the culprit.

Here's a simple assignment example where you might expect one thing, but get something totally different:

``` ruby Ex. 1 "and versus &&"
a = 2 and b = 4
puts "a = #{a}   b = #{b}"
#=>a = 2   b = 4
```

Ok, sure. But what about this?

``` ruby Ex. 2 "and versus &&"
a = 2 && b = 4
puts "a = #{a}   b = #{b}"
#=>a = 4   b = 4
```

Woah...different.

Well, it makes perfect sense if you refer to your handy table of order of precedence. Here is what happens chronologically in Ex. 1:

1) the value 2 is assigned to the variable 'a'<br>
2) the value 4 is assgined to the variable 'b'

or 

``` ruby Ex. 1 Expressed parenthetically
(a = 2) and (b = 4)
```

Since '=' has a greater precedence than 'and' this makese sense.

In Ex. 2:

1) the value 4 is assigned to the variable 'b'<br>
2) '2 && 4' is evaluated, returning 4<br>
3) the value 4 is assigned to the variable 'a'

or

``` ruby Ex. 2 Expressed parenthetically
a = (2 && (b = 4))
a = (2 && 4) #simplified
```

Once again it all comes down to '&&' having a higher order of precedence than '=' whereas that of 'and' is lower than that of '='.

In step 2 in Example 2 you'll notice that '2 && 4' returns '4'. That is due to the <strong>Associativity</strong> of '&&' which is left-to-right. This means '2' is evaluated first, followed by '4' which is returned.

Finally, here's another quirk you might come across in Ruby's precedence rules:

``` ruby Ex. 1 "&&/|| vs and/or"
true or true and false
#=>false
```

while 

``` ruby Ex. 2 "&&/|| vs and/or"
true || true && false
#=>true
```

The difference in return values here boils down to 'and' and 'or' having identical precedence resulting in Ruby evaluating it left-to-right while '&&' having a higher precedence than '||' means 'true && false' receives first evaluation resulting in a 'true || false' that returns true.

In precedence, as with everything else in Ruby there are no surprises, so long as you know what to expect.