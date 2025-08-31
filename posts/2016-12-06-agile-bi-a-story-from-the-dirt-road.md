# Agile BI, a story from the dirt road
#### 12/06/2016

So much has been written about agility in software development that I was really wondering what I could add that brings a little value or 
clarity about the process and its application to Business Intelligence and Data Science. Here is a little story ...

**The Story**

As a TV host, I want to ride a motorcycle from Yellowknife to Punta Arenas so that I can film a documentary.

**The Vision**

I am thinking a Harley-Davidson, with all the bells and whistles.

**Agile development is not like this:**

![pic2](/img/waterfall-bike.jpeg)

In this mode, your first day on the road will be when the last bolt is tighten on the last day of the building process. You better not have change 
your mind and still want a Harley ... even if you discovered that you will most likely ride on dirt roads and across mountains.

**Agile development is like this:**

![pic3](/img/agile-bike.jpeg)

Agile is not about working faster. It is about frequently delivering small usable software increments that gives the business more opportunities 
to provide feedback and adjust priorities.

With short iterations ...

* You can start travelling sooner
* You may end with a different motorcycle matching your real needs
* You may choose to stop the project at the scooter or the dirt bike
* You can find issues early, when investment is at a minimum (are the roads open?, is fuel available?, where can I find spare parts?)

**Always aim for increasing users' happiness**

In the end, Business Intelligence is about having your end-users feel happy and empowered to have a solution at their fingertips that helps 
them answering the questions they have. In Data Science, it is about making other applications add value to the business by 
behaving dynamically. This can take many forms like a web page recommendation, an adaptive call center script, or something l
ike a scoring algorithm to determine which customers to make an offer to.

But how do you get there? It’s a *long* drive from Yellowknife to Punta Arenas… How to avoid the Big Bang approach and the familiar 
paralysis and waste that it creates?

First of all: start small. Identify the most valuable **little** piece of software you can build, and then do it. 
Practice [dirty data modeling](https://sdeblois.github.io/2016-11-14-dirty-data-modeling/), get involved and *focus* on this small 
but valuable little piece of software that you want to build. Following agile practices, you want this first software iteration to stand by itself, to be executable and to *do* something for the business (like this kick scooter). Using the 
first iteration to build the backend of a Harley-Davidson will not bring much value in the short term, because it just can't run 
and generates zero useful feedback.

The principle of starting small and building fully executable little increments of software is based on the idea that no amount 
of meetings, documents, or contracts, can replace having users driving the software, and providing real feedback. Software delivery 
surprises are an unavoidable fact so delivering working software in small increments lets your users provide very early feedback 
that is usually easy to integrate in the next increment ... while it is still cheap to do so.

***It's all talk until the code runs***   -- [Ward Cunningham](https://en.wikipedia.org/wiki/Ward_Cunningham)

By riding the kick scooter end-users get a better idea of what they are looking for in a bicycle (maybe having a way to brake, and 
something to sit on would be nice). Looking through the window at the first workstation of a Harley-Davidson plant will not tell you 
much about your real needs, and certainly offers nothing in the way of experiencing the ride.

**There is also something for the data engineer**

On the technical side, there is also a lot of value in knowing very early where your architecture is great, and where it is not quite 
right. By delivering the first few small increments all the way to the end-users, you are forced to go through all your data layers, 
servers and tools. You will learn what works well and what doesn’t work so well, and you will be able to adjust or create some 
proof-of-concepts while it is still cheap to do so. You might also prove that some of your ideas are really smart. We often build 
the first few increments as an open acknowledgement of doing prototyping, and we let the architecture emerge through the 
results of our development. As [Brooks](https://www.amazon.com/Mythical-Man-Month-Essays-Software-Engineering/dp/0201006502/ref=sr_1_2?ie=UTF8&qid=1480690402&sr=8-2&keywords=mythical+man+month) wrote, some 40 years ago: build 
one to throw it away. It is still true today but it is a little different. What we deliver today is a small increment of software 
and if we have to throw it away we are only wasting a small amount of time and energy. We are not wasting our investments in 
the previously delivered increments. Also, the more increments you deliver the more you learn and you are less likely to 
throw away the next increment you build.

Another side effect of using small development increments is that it opens the door to discovering your foundational needs. You may 
discover that using those 3 fact tables and 7 dimensions gives you 95% of the value you can expect from your solution. You can now 
make a well-informed decision about investing time and money to go after this last 5% value. Is it really worth it? Or should we 
focus on another business area instead? In a lean software development context, it eliminates waste in development and maintenance 
of low value deliverables. Just like Ian Rogers in [My Road is Your Road](http://myroadisyourroad.tumblr.com/) you might even discover 
that a dirt bike is really more suitable than a Harley-Davidson to ride through the forests and mountains…

![pic4](/img/punta-arenas-trail.jpg "Punta Arenas")
