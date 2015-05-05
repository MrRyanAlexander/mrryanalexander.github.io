---
title:  "Solving JuggleFest by Yodle"
date:   2015-04-28 20:54:11
level: "Entry Level"
tags: "Python"
---

Today I will begin working on ways to solve the JuggleFest problem by Yodle in Python. The first commit I pushed can be found [here][fist_commit]. 

This problem requires that I read in a file, line-by-line and do some work with the result. So first I need a simple way to read in a file. Python has a built in method called, open and takes a file argument and another optional argument for reading/writing. 

{% highlight python %}
f = open('file.txt', 'r')
{% endhighlight %}

I also need to format each line into useable data. All I need from each line are the int values obtained by using a regex to extract '\d+' - all of the digits - and int() which takes a number string and converts it into useable integers. 

{% highlight python %}
[int(i) for i in re.findall(r'\d+', l)] 
{% endhighlight %}

The input file contains circuits at the top and jugglers at the bottom. The two sections are seperated by a space. If I check for that space, I know I have finished obtaining the circuits when I find it. So I will use that as a starting point for knowing where I am in the file. 

{% highlight python %}
if line == '\n':
{% endhighlight %}

Now I have a way to read the file and know which section I am currently reading. The next part is to start computing the dot products. In my first iteration I saved all of the dt products and looped over them for matches. Can you imagine how bad that was? Just think about it. There are 2000 circuits and 12000 jugglers. If I compute a dot product for each jugglers preferences and then loop over that data for matches, I will potentially loop millions of times. That will crash my computer. 

Update: 5/1/15

The best way I have thought of so far is to model this as a type of first in last out pattern. Now given that I really don't fully understand what the means, I will just work though my own version of it. I will use Classes, one for Jugglers and another for Circuits. I will make the Juggler class have a default method to compute its needed dot products and a method to enter it into a circuit. When a Juggler enters a Circuit, the Circuit will haze the inductee by testing for a match. This works making Circuits have a list of matches. If no matches exist, we can just append a Juggler, but if matches exist, we check if this Jugglers Dot product for this Circuit is higher than any others. If so we insert it before else we append it. When there are too many Jugglers or this one is not matchable, we pass it to its next preferred Circuit. By the time we have read in the file, all of the Jugglers we created will have entered Circuits and the Circuit hazing will have determined all of the matches. 


{% highlight python %}
openCircuit()
{% endhighlight %}


To see the code I created for the above concept, [click here][code]

At the end I want to print out the details in a nice way, so I created little Class helpers. The requested value of the Jugglers assigned to Circuit 1970 is also printed out. 

{% highlight python %}
print "C"+str(c.t), m.prettyPrint()+",",
print circuits[1970].cmnt()
{% endhighlight %}

[first_commit]: https://github.com/MrRyanAlexander/JuggleFest/blob/ca2d8d67f69add5b03918a9473b593b17e13d4b3/juggle.py/
[code]: https://github.com/MrRyanAlexander/JuggleFest/blob/master/juggle.py
