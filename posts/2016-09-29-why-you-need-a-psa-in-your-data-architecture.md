---
layout: post
title: Why you need a PSA in your data architecture?
---

In my current data systems, I usually create a persistent staging area (PSA) that receives 
raw/untransformed data, keeps all of it (all history), in the format we receive it (zip, json, csv, etc), etc. That first layer 
is very important because anything else you generate from it implies human decisions that transform the data ... and those decisions 
can (will) be wrong and will need to be changed. The PSA is the key to maintain an agile data workflow where prototyping and 
experiments are possible. 

Using the PSA, no matter how "bad" you transform your data, you can just fix the transformation code and re-run. The cheap storage and 
increasing speed of today's data tools (like HDFS, Apache Spark and many others) allows to move away from the "physical" Data Warehouse 
that gets loaded incrementally. We are at a point where we can build "just-in-time" data warehouses that serve the purpose of integrating 
the data to generate the final serving tables (flat, dimensional, etc.) ... and then can be deleted. This virtual DW architecture also lets you do prototyping on the design of the DW _itself_, which is very powerful. 

The Persistent Staging Area can also feed the Lambda Architecture's Master dataset as defined by Nathan Marz in his [Big Data](http://www.manning.com/books/big-data) book.

I was inspired to write this article after reading [Do you feel torn (too)?](https://tombreur.wordpress.com/2016/09/28/do-you-feel-torn-too/) by Tom Breur where 
he explores the need for keeping a pristine (raw) version of our business facts (the PSA) combined with an agile (and fast enough) way of presenting the data to the 
end-users. By being more agile and more responsive we will decrease the tendency for the end-users to request access to the raw data and create silos of 
alternate realities.

Below, Humanity's PSA, [The Svalbard Seed Vault](https://www.croptrust.org/what-we-do/svalbard-global-seed-vault/)

![seed-vault](/img/svalbard-seed-vault.jpg "The Svalbard Seed Vault")
