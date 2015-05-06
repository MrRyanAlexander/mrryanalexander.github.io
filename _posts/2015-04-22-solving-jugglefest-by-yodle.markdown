---
title:  "Solving JuggleFest by Yodle"
date:   2015-04-28 20:54:11
level: "Entry Level"
tags: "Python"
---

Today I will begin working on ways to solve the JuggleFest problem by Yodle in Python. The first commit I pushed can be found [here][first_commit]

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

Now I have a way to read the file and know which section I am currently reading. The next part is to start computing the dot products, but first I need to understand how to solve the problem. As of right now, I don't have a clue. I've never solved a problem like this before and since I don't have any knowledge of math beyond the basics, I have no reference for where to begin. I will find a way though, so what I am going to do is draw out a list of the dot products for the example data set. 

The code I have started writing for this is too much to add here, so you will need to head over to my github and follow my commit history. [history][first_commit]

In my first drawing, I compute the first preferred dot product for each juggler to look for some type of pattern in the list. I put each one of these dot products into a table - the one on top - and with it I am figuring out that the dot products are not ordered by totalling them up and putting them in order. For each circuit I computed the dot products for each juggler and then I added up each jugglers dot products. Now I put them into the first circuit that was preferred. So for example, lets say that for juggler J0, the total of her circuit dot products - 102, 31, 18 - is 151 and her first preferred circuit is 0. We would put her total score after 251 in the top right of the top table. I think this is totally wrong. I am lost and trying to find my way. I am sure you can see that if you know what I should be doing. Tomorrow I hope to make more progress that I did today.

![drawing](/img/first.jpg)

Update: 4/30/15

Yesterday didn't bare that much fruit, but I did learn one way that I cannot solve this. The dot products are not sorted by totalling them up. LOL That will only matter at the end getting circuit 1970.  

I've already been at working on this for half of that day. That "jump start" feels like it was yesterday at this point. This is harder than I thought it would be and I am still staring at the same drawing from yesterday. I want to quit right now, but I know I need to continue. If I can figure this out, I know it will boost my confidence and help me pursue other tough problems that I have been avoiding. How should I do this? If I had finished school this would be easier. If I had friends who cared about this stuff, this would be easier. I have to take the hard route. There must be a way to solve this. Maybe if I add up all of the other circuit and dot product combinations and put them all into another list, but bigger and with everything, maybe then I will see a pattern. Maybe then this will start making sense. I'll add the drawing here when I finish it. 

![drawing](/img/second.jpg)

Man I am pulling out hair over this now. I really thought that there would be some visible pattern by doing that, but nope. I'm gonna call it a night and maybe tomorrow this will start making more sense. 

Update: 5/1/15

Okay! Hello World! Today is a new day and I am ready to start off fresh with this again. I woke up with an idea today. I love to drink coffee first thing in the morning, while I talk with guests and vape. So I made sure to get my morning fixes in before diving into this. I feel very clear headed right now, so today will be a great day to make some serious progress towards understanding this. Okay, enough with all this rattling away at the mouth bs, lets talk about the JuggleFest. My idea is to make another list, but in this list I will create 3 columns and in each I will orderly list each jugglers dot product by preference. I noticed that in the example, each juggler is ordered based on the circuit value, not the preference, so maybe this will lead to some understanding. 

![drawing](/img/third.jpg)

I don't think sorting by and selecting all of these jugglers will work out in the end. So far I am noticing something that will probably lead to code that will crash my machine. I think I am looping bad. By that I mean that maybe there is some other way to sort, search and select jugglers other than by looping this list. For now that won't be an issue, but with a bigger list - the one for the JuggleFest has 12K and 2K lines of data - I may be totally screwed. That could be too many I think. Not sure how many loops this is, but I am estimating it's in the millions. Well anyway, I know I have to figure out some way to to get each one of these things in the right columns at the end. By columns I mean circuits. I know the way I write and think is a bit absurd, but so are you, so stfu and keep reading. ;) Maybe you will catch a glimps of me changing, as that is kinda why I made this. I use Sublime for everything except for Obj-C and Java, so being able to have one tab open with code and another to write these posts is, can we say, "FUCKING AWESOME"!. Okay, back to coding. 

I pushed a commit out just now, so I'll also link to it [here][second_commit]. Init you will note that I am still using those 4loops I mentioned earlier. I know they are bad, but I don't know what to do about them just yet. I also still haven't figured out how to solve this yet, but I think I am getting closer. Each juggler prefers circuits A,B,C and each circuit accepts 4 jugglers. I know that to start the first jugglers preference matters because that determines how low the other ones must be. So if, out of all jugglers first preferences, the highest dot product for C0 is 31, all remaining matches must be below 31. I will work off of these beliefs for now, but if I end up being wrong, I will note that later. I tend to be wrong a lot, so I don't mind admitting where I f-it up. 

Update 5/2/15

OMFG! I think I got it now. First off, let me just say that this has been an exausting learning experience, but I am glad I stuck it out until now because what I am working on right now is going to be f-n awesome when it is done. Last night I hung out with friends, drank and smoked some herb. Yeah! I am an herbal programmer, get over it. I've read about people dreaming in code and having very odd eureka moments, well I just had one. When I came back to my place and plopped down on my bed, I grabbed that piece of paper I wrote out all of the jugglers dot products on. If you haven't been following along, it's the second picture in this post. Well guess what I noticed. Let's pretend that there are 10 additional jugglers in the example and out of them most of them are lower in value than those currently in the example. However lets pretend that just enough of them prefer C2 more than J6. J6 has preferred C1 second, but lets pretend it's too high for that circuit and heads to it's 3rd choice, where it is the highest of all matches for C0. That would force J5 to be the 2nd match. I wrote a little about this in my code too because by realizing this, I know I can finish this now. I started off completely blind a few days ago. This is my first algorithm on my own and ironically I know I can write it now because of one detail; J6. This also negates my prior knowledge as I was wrong to assume the preference order matters. It does matter, but not in the sense I was thinking before. I thought that the first preference defined the highest value for that circuit, but nope, it's just a pass. Basically if I just add jugglers to their preferred circuit starting with their first. If the circuit is empty, I just add a juggler. If it's full I check values for it being greater than. If it's greater than any in the circuit, I insert it, and pop/pass the extra juggler; the lowest value. If it's not greater than any of them I pass it to its next preference where once again we compare it based only on that circuit. This might sound convoluted to you, but it all makes sense to me now. 

Pushed Working Solution : [commit][third_commit]  

![drawing](/img/forth.jpg)

I had a little fun with this. Instead of just showing a solution with a few simple iterations, I made a Circuit class and a Juggler class. For the circuits I just setup empty circuits with a few values for each line reading the top of the file. For jugglers it's different. Each line where I create a juggler starts off a match. Since the Juggle Fest is really a make believe competition between fictious jugglers that enter circuits with different abilities, I wrote code that lightly emulates that scene. I love games, but not so much playing them as I do planning and creating them. So the way I wrote the code is from the point of view of it being an actuall competition. Jugglers enter circuits and request premission to compete. If the circuit is empty, they just get told to sit down and stfu. If there is competition though the circuit leader sends the juggler through a series of hazes to see how well it matches up against the rest of the pack. In the end the circuit either accepts the juggler and it's abilities or it kicks it out by passing it to another circuit. Every juggler created goes through all of that and at the end we have the list. 

I know I made this harder than it is, but I learn like that and I sure learned a lot here. Now I know a simple way to sort any list; never sort it. I do wonder how I may be able to know if X is > L for L in M without comparing X to every L. Maybe that will be my next post, but that's another project.  
{% highlight python %}
openCircuit()
{% endhighlight %}

[My JuggleFest solution][code]

I created little Class helpers I called prettyPrint(). 
The requested value of the Jugglers assigned to Circuit 1970 is also printed out. 

{% highlight python %}
print "C"+str(c.t), m.prettyPrint()+",",
print circuits[1970].cmnt()
{% endhighlight %}

![drawing](/img/fifth.jpg)

[first_commit]: https://github.com/MrRyanAlexander/JuggleFest/commit/ca2d8d67f69add5b03918a9473b593b17e13d4b3/
[second_commit]: https://github.com/MrRyanAlexander/JuggleFest/commit/bad7657c98af2bbc965ca556850130750b542f10/
[third_commit]: https://github.com/MrRyanAlexander/JuggleFest/commit/cd6dc4c960ae28d36b16ae84cacc7629e208b81d/
[code]: https://github.com/MrRyanAlexander/JuggleFest/blob/master/juggle.py/
