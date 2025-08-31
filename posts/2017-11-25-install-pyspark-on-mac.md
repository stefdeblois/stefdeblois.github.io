# Install PySpark on Mac
#### 11/25/2017

Here are the steps to follow to run Python, Pandas and PySpark on a Mac:

### Install Java JDK 8

* At the time of writing this, Java JDK 9 is not compatible with PySpark.
* The JDK 8 is downloadable [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* In your bash_profile you should see (if not, add it yourself):
  * export JAVA_HOME=$(/usr/libexec/java_home)

### Install Anaconda

* With Anaconda you get Python, Pandas and the most useful libraries for data manipulation.
* Anaconda is available [here](https://www.anaconda.com/download).
* At the time of writing this, I downloaded Anaconda2 (Python 2.7), Graphical Installer.
* Anaconda will automatically add a PATH to your bash_profile.

### Install Apache Spark

* You download Apache Spark [here](https://spark.apache.org/downloads.html).
* At the time of writing this, I downloaded version 2.2.0, Pre-built for Apache Hadoop 2.7 and later.

![Spark](/img/spark-download.jpeg)

* Unzip, and move the unzipped folder to your Home folder.
* In your bash_profile, add this line and change it to your Spark folder:
  * export SPARK_HOME=~/spark-2.2.0-bin-hadoop2.7
  
* At this point, if you open a new terminal window and type "pyspark", you should see PySpark start at the command line.

![Spark](/img/pyspark-terminal-start.jpeg)

### To start PySpark and directly open a Jupyter Notebook

* Add two lines to your bash_profile:
  * export PYSPARK_DRIVER_PYTHON="jupyter" 
  * export PYSPARK_DRIVER_PYTHON_OPTS="notebook" 
  
* Now, when typing PySpark in a new terminal window, PySpark will initialize and start a Jupyter notebook.
* If you create a new Python notebook and type "sc" in a cell and excute the cell, you should see the Spark context information.

![Spark](/img/pyspark-sc-context.jpeg)

* You are ready to start coding.
