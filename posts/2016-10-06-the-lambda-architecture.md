# The Lambda Architecture ... Speed and Agility
#### 10/06/2016

For experienced data architects processing data for data warehouses and business intelligence solutions, we have been used to think “incrementally”. We have been creating complex data models and incremental load processes that are effectively required to work around the limitations in storage and speed of our databases and ETL tools.

When building incremental data architectures, you have to handle the eternal patterns:

![pic1](/img/incremental-data-patterns.jpg "Pic 1")

Those patterns can get very complex quickly. You usually have to generate an expiration time for each row to simplify your SQL querying. You also often need to handle a row status of “active” or “expired” if you do logical deletes. Those changes require updates to existing rows, which is expensive.

With the advances in cloud technologies, massively parallel processing databases and in-memory data processing tools; we have now reached an era where we can build our architectures closer to the foundational nature of data.

As part of this trend, Nathan Marz described something called “The Lambda Architecture” in his book [Big Data](http://www.manning.com/books/big-data). It consists of replacing those complex incremental processes by processes that re-create the end-users tables by reading “all the data” every time they run. Building your data architecture this way simplifies your workflow. Coding errors can be fixed by changing the code and re-running the process (no more cumbersome database manipulations required to put the data back to a previous state for restart). Business users can evolve their transformation rules with agility; you just change the code and re-run. The processes are becoming fast and efficient because all they do is insert data, no more updates or deletes required.

The Lambda Architecture + a Permanent Staging Area (PSA):

![lambda-architecture](/img/gv_lambda_architecture.jpg "Lambda Architecture")

The key to achieve this “agility” is to make the staging data permanent and immutable. It means that you always add new data to your staging repository. You never replace or delete existing staging data. Also, essential, you never transform the staging data when extracting it from the sources. If you are transforming the data on its way to the staging data repository, you are applying “human” decisions to the data and those will be wrong, sometimes. Those transformations belong in the batch layer. By protecting the staging dataset, you are protecting your solution against pretty much everything that can go wrong (basically, you can rebuild everything from it).

This data architecture includes many objects...

The **sources** could be any data providers that you need for your solution: databases, text files, APIs, Queues, HTML scraping, etc.

The **staging process** receives the data from the sources and stores it "as-is", permanently and untransformed in the staging data repository. As an example, the new data files could be added to a folder structure in HDFS or Amazon S3 describing the data sources and the "time". The new data files are always added to the staging data, often by adding a file to an existing folder. The staging data is immutable so you never update or delete existing files.

The **staging data** repository serves the data appropriately to the batch layer and the speed layer. For real-time scenarios, the staging data could use queuing and streaming technologies.

The **master process** receives the new staging data and integrates it in the master data repository using a temporal and immutable business model like a data vault, a fact-based model or a graph database. The master data repository can also be implemented as a distributed file system because of its append-only nature. Temporal calculations are expensive so the master data will often be loaded incrementally. Even if the master data is loaded incrementally, the master process should be designed to fully re-create the master data, if needed, by simply deleting it.

The **master data** repository serves the data to the batch process.

The **batch process** is always reading ALL the master data and then completely re-computes the tables that will be served to the end-users. Internally, in the batch process, you often create some kind of light “just-in-time” data warehouse that supports more complex data integration requirements. The “just-in-time” data warehouse supports “compute once, re-use multiple time” tables that you need for other steps in the batch process. The resulting batch tables are published to the serving layer. When using tools like Apache Spark, this “just-in-time” data warehouse will exist in memory and it will vanish when the batch process is done.

The **speed process** supports the need for real-time visualization. It receives the data that require fast publication and processes it in real-time, landing the resulting data in speed tables in the serving layer. The speed layer exists because the batch process, in some scenarios, can be running for a few hours. In some cases, that gap must be filled so people can query the real-time information that they need. As a result, often, the speed data is not as rich as the batch data but it serves its purpose of broadcasting very recent events. The next time the batch process runs, the previously “speed loaded” data will now be part of the richer, better batch data and the cycle continues.

The **serving process**’s role is to merge the data from the batch and speed tables into one structure that the end-users can access. In other words, you are presenting the batch data that may be a few hours old, next to the real-time speed data, into one simple interface. For example, this can be achieved with “union” views in Amazon Redshift but different tools handle this differently.

In conclusion, the Lambda Architecture is a really good concept to explore when you want to simplify your data architecture and handle larger and larger data sets. It also works really well for a smaller scale data warehouse where it simplifies its development and maintenance immensely. By adding a permanent staging area to the architecture we increase the agility of the batch layer. Around the corner, there is also some other architecture that focuses on seeing all the data as a real-time stream. This is something to keep an eye on but they are may be adding too much complexity for regular information management needs … for now.

