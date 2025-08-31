---
layout: post
title: Decision Support Systems
subtitle: A Generic Architecture
---

An architecture supporting a Decision Support System (DSS) contains multiple roles, repositories and processes working together to transform your raw data into business information.

![Decision Support Systems Architecture](/img/dss_generic_architecture.jpg "Decision Support Systems Architecture")

Let's explore each component ...

![Casting Call](/img/casting-call.jpg "Casting Call")

#### The 5 roles of a Decision Support System:<br><br> 

* **Data Suppliers**: who push source data to the system or is accepting pull requests from the system.<br><br> 
* **Data Consumers**: who are using the curated part of the system to answer their queries or who are receiving pushed alerts and reports from the system. They are your BI tool users, alert email recipients, canned reports recipients, query writers, etc.<br><br> 
* **Data Explorers**: who are using the structured part of the system to explore raw data and derived value from their findings. Those are your data scientists, actuaries, data analysts, etc. Their valuable findings will be automated by the data engineering team.<br><br> 
* **Data Administrators**: who monitor and maintain the day to day operations of the system. They manage the master data.<br><br> 
* **System Administrators**: who monitor and maintain the day to day operations of the system. They also investigate and fix bad files.<br><br> 

![sp](/img/screenplays.jpg "sp")

#### The 6 repositories of a Decision Support System:<br><br> 

* **New Files**: where pushed and pulled files are landed until they get ingested.<br><br> 
* **Master Files**: where the raw untransformed files are archived forever. This repository is immutable and can be use to recompute all the downstream repositories.<br><br> 
* **Structured Files**: where the master files are transformed into structured queryable files. For example, exploding and flattening json files into parquet files. This repository support data exploration and downstream transformations.<br><br> 
* **Rejected Files**: where files that can't be structured are stored until further investigation. When fixed, they are sent back to the master files for another structure attempt ... or they are kept here if they are useless.<br><br> 
* **Integrated Files**: where the files are transformed into an integrated time-variant business model.<br><br> 
* **Curated Files**: where the Integrated Files are transformed into customized queryable datasets served to the data consumers.<br><br> 

![swl](/img/star-wars-lead.jpg "swl")

#### The 6 lead processes of a Decision Support System:<br><br> 

* **Land**: processes, often managed by the data suppliers, that push data to the new files repository. This can also be processes, managed by the system administrators, that pull data from the data suppliers into the new files repository (often by calling an API).<br><br> 
* **Ingest**: processes that move the new files into the permanent master files repository. In theory, you could just ask the data suppliers to land directly into the master files repository because no transformation happen ... but in reality your master files repository is very precious and it is better to create this "new files" buffer to make security requirements easier to maintain.<br><br> 
* **Structure**: processes that find new master files and structure them to make them queryable. This is where you apply "expensive" transformations like unzipping, parsing json, etc. The content itself is not transformed and remains raw. The files that can't be structured are moved to the rejected files repository.<br><br> 
* **Integrate**: processes that read the structured files and transform its data into an integrated time-variant data model supporting the business function.<br><br> 
* **Curate**: processes that read the integrated files and generate curated datasets served to the data consumers.<br><br> 
* **Serve**: processes that serve analytics information to the data consumers through their query tools or BI tools. They also send Business Alerts to the Data Consumers. If unexpected results are presented to the consumers, they will send system alerts to the system administrators. The serve processes will also update the MDM database if required (new lookups to define, new descriptions, etc).<br><br> 

![sws](/img/star-wars-red-1.jpg "sws")

#### The 3 supporting processes of a Decision Support System:<br><br> 

* **Manage**: this process use a user interface to let the data administrators update the master data by adding, new lookup values, new descriptions, etc. It is basically where you create the data that have no source.<br><br> 
* **Fix**: this process let the system administrators investigate rejected files, fix them and republish them to the master files repository to get structured. As much as we dream of automation, the thousand ways a file can be bad will most likely force this process to be manual.<br><br> 
* **Explore**: this process is mostly the only thing we hear about in today's news: artificial intelligence, machine learning, deep learning, data science, etc. Those activities are based on exploring raw data, generating results and evaluating the value and feasibility of using those results in your day-to-day operations. When your exploration results are meaningful, the data engineering team integrate those algorithms and calculations into the normal flow (land -> ingest -> structure -> integrate -> curate -> serve).<br><br> 
