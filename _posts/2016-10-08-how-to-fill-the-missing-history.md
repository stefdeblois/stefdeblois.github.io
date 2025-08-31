---
layout: post
title: How to fill the missing history?
---

In data warehousing, temporal data models and data flows have a real tendency to become complex very quickly. Adding to this, you may have to handle multiple disparate data sources 
that do not merge very well. You may want to load the same type of business events from multiple sources and run into missing attributes that creates blanks in your 
final serving tables.

------

Below is an oversimplified example of a lazy data integration:

![fbm-lazy-example](/img/fbm_lazy_example.jpg "Lazy Data Integration")

"Sales Source 1" only knows the class of a user (Silver or Platinum).

"Sales Source 2" only knows the city of a user.

Let's say you do a lazy integration of the two sources by just appending them:

- Yes, you get a complete dataset of all the "sales" events ...

- but all the missing attributes are unknown (?)

- Yes, this new dataset represents the exact reality of the source data ...

- _but is it the business reality?_

If you look at the two reports created from this dataset you can easily see how bad the results are. A lot of sales are going to the "unknown" buckets. You can bet 
this is not the business reality.

------

Now, lets's look at this example of a smarter way to integrate these data sources:

![smart-lazy-example](/img/fbm_smart_example.jpg "Smart Data Integration")

First, you need to generate more accurate information about a user. To achieve this:

- you create one table by user attribute

- you read the two data sources and you load the history of each attribute

- not showing here, but you may also have duplicate user attributes, for example user\_name, coming from different sources and they can be integrated the same way

From this process you get two tables:

- User Class History

- User City History

Physically, those tables can be adapted to your current data modeling flavor. They can be attribute tables in an anchor model, satellite tables in a data vault model or 
simply fact-based tables as described in the [Big Data](http://www.manning.com/books/big-data) book (chapter 2). They can also be in-memory lookup tables in a Big Data flow.

Now, you read and load the sales sources into the "Smart Data Integration" table but you use the user\_id and the sales\_time to lookup the right value for the 
user\_class and user\_city.

This lookup process will actually fill the blanks (in red). It will assume that if you heard from source 1 that the user is a Silver member at a specific point in time, you can safely 
assume that he was a silver member at the same point in time in source 2.

The reports generated from this more accurate dataset are now much more representative of the business reality. We still see an "unknown" city for a transaction made 
on 3/15/2015 because there was no city information available at that point in time. The business may decide to fill this blank by assuming that the first city seen 
in the sources is to be use in that case. This is perfectly fine; this is their business rule.

A side effect of this design is to make reporting datasets more resilient to attributes that suddenly disappear from one source but are still seen in other sources.

As you can see, this process requires smarter coding of your data workflow, but the reward is a more accurate representation of your business data.
