# PySpark Pocket Guide
#### 11/11/2018

### create a two columns dataframe from a list


<br>


```python
myschema = ["customer_id",\
            "customer_name"]

mydata = [(101,"Andre"), \
          (202,"Katy"), \
          (303,"Robert")]

dfCustomer = spark.createDataFrame(mydata,schema=myschema)
dfCustomer.show()
```

	+-----------+-------------+
	|customer_id|customer_name|
	+-----------+-------------+
	|        101|        Andre|
	|        202|         Katy|
	|        303|       Robert|
	+-----------+-------------+
    


<br>

### create a one column dataframe from a list

<br>


```python
mylist = [("Richmond",),("Dallas",)]
myschema = ["city_name"]
dfCity = spark.createDataFrame(mylist,schema=myschema)
dfCity.show()
```

    +---------+
    |city_name|
    +---------+
    | Richmond|
    |   Dallas|
    +---------+
    


<br>

### create a dataframe from a csv file

Given this singers.csv file:<br>
firstname, lastname, cityname<br>
"Elvis", "Presley", "Memphis"<br>
"John", "Lennon", "Liverpool"<br>


```python
dfSingers = spark.read.csv("singers.csv",header=True)
dfSingers.show()
```

    +---------+--------+---------+
    |firstname|lastname| cityname|
    +---------+--------+---------+
    |    Elvis| Presley|  Memphis|
    |     John|  Lennon|Liverpool|
    +---------+--------+---------+
    


<br>

### add a new column

<br>


```python
from pyspark.sql.functions import col,lit,concat
mylist = [("Elvis","Presley"),("John","Lennon")]
myschema = ["Firstname","Lastname"]
dfSingers = spark.createDataFrame(mylist,schema=myschema)
dfSingers.show()
```

    +---------+--------+
    |Firstname|Lastname|
    +---------+--------+
    |    Elvis| Presley|
    |     John|  Lennon|
    +---------+--------+
    



```python
# derived a column from other columns
dfSingers = dfSingers \
    .withColumn("Fullname",concat(col("Firstname"),lit(" "),col("Lastname")))
dfSingers.show()
```

    +---------+--------+-------------+
    |Firstname|Lastname|     Fullname|
    +---------+--------+-------------+
    |    Elvis| Presley|Elvis Presley|
    |     John|  Lennon|  John Lennon|
    +---------+--------+-------------+
    



```python
# add a literal value to a column
vDecade = "60s"
dfSingers = dfSingers \
    .withColumn("Decade",lit(vDecade)) \
    .withColumn("Style",lit("Rock 'n' Roll"))
dfSingers.show()
```

    +---------+--------+-------------+------+-------------+
    |Firstname|Lastname|     Fullname|Decade|        Style|
    +---------+--------+-------------+------+-------------+
    |    Elvis| Presley|Elvis Presley|   60s|Rock 'n' Roll|
    |     John|  Lennon|  John Lennon|   60s|Rock 'n' Roll|
    +---------+--------+-------------+------+-------------+
    


<br>

### update columns

<br>


```python
from pyspark.sql.functions import col,upper,ltrim
mylist = [("          Elvis","          Presley"), \
          ("           John","           Lennon")]
myschema = ["Firstname","Lastname"]
dfSingers = spark.createDataFrame(mylist,schema=myschema)
dfSingers.show()
```

    +---------------+-----------------+
    |      Firstname|         Lastname|
    +---------------+-----------------+
    |          Elvis|          Presley|
    |           John|           Lennon|
    +---------------+-----------------+
    



```python
dfSingers = dfSingers \
    .withColumn("Firstname",ltrim(col("Firstname"))) \
    .withColumn("Lastname",ltrim(upper(col("Lastname"))))
dfSingers.show()
```

    +---------+--------+
    |Firstname|Lastname|
    +---------+--------+
    |    Elvis| PRESLEY|
    |     John|  LENNON|
    +---------+--------+
    


<br>

### rename a column

<br>


```python
mylist = [("Elvis","Presley"),("John","Lennon")]
myschema = ["name1","name2"]
dfSingers = spark.createDataFrame(mylist,schema=myschema)
dfSingers.show()
```

    +-----+-------+
    |name1|  name2|
    +-----+-------+
    |Elvis|Presley|
    | John| Lennon|
    +-----+-------+
    



```python
dfSingers = dfSingers \
    .withColumnRenamed("name1","Firstname") \
    .withColumnRenamed("name2","Lastname")
dfSingers.show()
```

    +---------+--------+
    |Firstname|Lastname|
    +---------+--------+
    |    Elvis| Presley|
    |     John|  Lennon|
    +---------+--------+
    


<br>

### drop a column

<br>


```python
mylist = [("Elvis","Presley"),("John","Lennon")]
myschema = ["Firstname","Lastname"]
dfSingers = spark.createDataFrame(mylist,schema=myschema)
dfSingers.show()
```

    +---------+--------+
    |Firstname|Lastname|
    +---------+--------+
    |    Elvis| Presley|
    |     John|  Lennon|
    +---------+--------+
    



```python
dfSingers = dfSingers.drop("Firstname")
dfSingers.show()
```

    +--------+
    |Lastname|
    +--------+
    | Presley|
    |  Lennon|
    +--------+
    


<br>

### select columns

<br>


```python
mylist = [("Elvis","Presley","Memphis"),("John","Lennon","Liverpool")]
myschema = ["Firstname","Lastname", "Cityname"]
dfSingers = spark.createDataFrame(mylist,schema=myschema)
dfSingers.show()
```

    +---------+--------+---------+
    |Firstname|Lastname| Cityname|
    +---------+--------+---------+
    |    Elvis| Presley|  Memphis|
    |     John|  Lennon|Liverpool|
    +---------+--------+---------+
    



```python
dfSingers = dfSingers.select("Firstname","Cityname")
dfSingers.show()
```

    +---------+---------+
    |Firstname| Cityname|
    +---------+---------+
    |    Elvis|  Memphis|
    |     John|Liverpool|
    +---------+---------+
    


<br>

### filter rows

<br>


```python
from pyspark.sql.functions import col
mylist = [("Elvis","Presley","Memphis"), \
          ("John","Lennon","Liverpool"), \
          ("Paul","McCartney","Liverpool"),
          ("John","Lydon","London")]
myschema = ["Firstname","Lastname", "Cityname"]
dfSingers = spark.createDataFrame(mylist,schema=myschema)
dfSingers.show()                          
```

    +---------+---------+---------+
    |Firstname| Lastname| Cityname|
    +---------+---------+---------+
    |    Elvis|  Presley|  Memphis|
    |     John|   Lennon|Liverpool|
    |     Paul|McCartney|Liverpool|
    |     John|    Lydon|   London|
    +---------+---------+---------+
    



```python
# filter
df1 = dfSingers.filter("Cityname = 'Memphis'")
df1.show()  
```

    +---------+--------+--------+
    |Firstname|Lastname|Cityname|
    +---------+--------+--------+
    |    Elvis| Presley| Memphis|
    +---------+--------+--------+
    



```python
# filter/and
df1 = dfSingers.filter("Cityname = 'Liverpool' and Firstname = 'John'")
df1.show() 
```

    +---------+--------+---------+
    |Firstname|Lastname| Cityname|
    +---------+--------+---------+
    |     John|  Lennon|Liverpool|
    +---------+--------+---------+
    



```python
# filter/or
df1 = dfSingers.filter("Cityname = 'Liverpool' or Firstname = 'John'")
df1.show() 
```

    +---------+---------+---------+
    |Firstname| Lastname| Cityname|
    +---------+---------+---------+
    |     John|   Lennon|Liverpool|
    |     Paul|McCartney|Liverpool|
    |     John|    Lydon|   London|
    +---------+---------+---------+
    



```python
# where (same as filter)
df1 = dfSingers.where("Cityname = 'Liverpool'")
df1.show() 
```

    +---------+---------+---------+
    |Firstname| Lastname| Cityname|
    +---------+---------+---------+
    |     John|   Lennon|Liverpool|
    |     Paul|McCartney|Liverpool|
    +---------+---------+---------+
    



```python
# filter/like
df1 = dfSingers.filter("Lastname like 'L%'")
df1.show()  
```

    +---------+--------+---------+
    |Firstname|Lastname| Cityname|
    +---------+--------+---------+
    |     John|  Lennon|Liverpool|
    |     John|   Lydon|   London|
    +---------+--------+---------+
    



```python
# filter/like/and
df1 = dfSingers.filter("Lastname like 'L%' and Cityname like '%ool'")
df1.show()  
```

    +---------+--------+---------+
    |Firstname|Lastname| Cityname|
    +---------+--------+---------+
    |     John|  Lennon|Liverpool|
    +---------+--------+---------+
    



```python
# filter/like/or
df1 = dfSingers.filter("Lastname like 'L%' or Cityname like '%ool'")
df1.show()    
```

    +---------+---------+---------+
    |Firstname| Lastname| Cityname|
    +---------+---------+---------+
    |     John|   Lennon|Liverpool|
    |     Paul|McCartney|Liverpool|
    |     John|    Lydon|   London|
    +---------+---------+---------+
    


<br>

### sort rows

<br>


```python
from pyspark.sql.functions import col
mylist = [("Elvis","Presley","Memphis"), \
          ("John","Lennon","Liverpool"), \
          ("Paul","McCartney","Liverpool"),
          ("John","Lydon","London"),
          ("Sean","Lennon","New York"),
          ("Julian","Lennon","Liverpool")]
myschema = ["Firstname","Lastname", "Cityname"]
dfSingers = spark.createDataFrame(mylist,schema=myschema)
dfSingers.show()      
```

    +---------+---------+---------+
    |Firstname| Lastname| Cityname|
    +---------+---------+---------+
    |    Elvis|  Presley|  Memphis|
    |     John|   Lennon|Liverpool|
    |     Paul|McCartney|Liverpool|
    |     John|    Lydon|   London|
    |     Sean|   Lennon| New York|
    |   Julian|   Lennon|Liverpool|
    +---------+---------+---------+
    



```python
# sort
df1 = dfSingers.sort("Lastname","Firstname")
df1.show()
```

    +---------+---------+---------+
    |Firstname| Lastname| Cityname|
    +---------+---------+---------+
    |     John|   Lennon|Liverpool|
    |   Julian|   Lennon|Liverpool|
    |     Sean|   Lennon| New York|
    |     John|    Lydon|   London|
    |     Paul|McCartney|Liverpool|
    |    Elvis|  Presley|  Memphis|
    +---------+---------+---------+
    



```python
# select and sort
df1 = dfSingers.select("Lastname","Firstname","Cityname").sort("Lastname","Firstname")
df1.show()
```

    +---------+---------+---------+
    | Lastname|Firstname| Cityname|
    +---------+---------+---------+
    |   Lennon|     John|Liverpool|
    |   Lennon|   Julian|Liverpool|
    |   Lennon|     Sean| New York|
    |    Lydon|     John|   London|
    |McCartney|     Paul|Liverpool|
    |  Presley|    Elvis|  Memphis|
    +---------+---------+---------+
    



```python
# select and sort, using a list of columns"
sort_columns = ["Lastname","Firstname"]
df1 = dfSingers.select(sort_columns + ["Cityname"]).sort(sort_columns)
df1.show()
```

    +---------+---------+---------+
    | Lastname|Firstname| Cityname|
    +---------+---------+---------+
    |   Lennon|     John|Liverpool|
    |   Lennon|   Julian|Liverpool|
    |   Lennon|     Sean| New York|
    |    Lydon|     John|   London|
    |McCartney|     Paul|Liverpool|
    |  Presley|    Elvis|  Memphis|
    +---------+---------+---------+
    


<br>

### select distinct

<br>


```python
from pyspark.sql.functions import col
mylist = [("Elvis","Presley","Memphis"), \
          ("John","Lennon","Liverpool"), \
          ("Paul","McCartney","Liverpool"),
          ("John","Lydon","London"),
          ("Sean","Lennon","New York"),
          ("Julian","Lennon","Liverpool")]
myschema = ["Firstname","Lastname", "Cityname"]
dfSingers = spark.createDataFrame(mylist,schema=myschema)
dfSingers.show()      
```

    +---------+---------+---------+
    |Firstname| Lastname| Cityname|
    +---------+---------+---------+
    |    Elvis|  Presley|  Memphis|
    |     John|   Lennon|Liverpool|
    |     Paul|McCartney|Liverpool|
    |     John|    Lydon|   London|
    |     Sean|   Lennon| New York|
    |   Julian|   Lennon|Liverpool|
    +---------+---------+---------+
    



```python
# select distinct
df1 = dfSingers.select("Cityname").distinct()
df1.show()
```

    +---------+
    | Cityname|
    +---------+
    |   London|
    |  Memphis|
    |Liverpool|
    | New York|
    +---------+
    


<br>

### conditional processing "split/union" or "when/otherwise"

<br>


```python
from pyspark.sql.functions import col,lit
mylist = [("Elvis","Presley","Memphis"), \
          ("John","Lennon","Liverpool"), \
          ("Paul","McCartney","Liverpool"),
          ("John","Lydon","London"),
          ("Sean","Lennon","New York"),
          ("Julian","Lennon","Liverpool"),
          ("Johnny","Clegg","Johannesburg")]
myschema = ["Firstname","Lastname", "Cityname"]
dfSingers = spark.createDataFrame(mylist,schema=myschema)
dfSingers.show()    
```

    +---------+---------+------------+
    |Firstname| Lastname|    Cityname|
    +---------+---------+------------+
    |    Elvis|  Presley|     Memphis|
    |     John|   Lennon|   Liverpool|
    |     Paul|McCartney|   Liverpool|
    |     John|    Lydon|      London|
    |     Sean|   Lennon|    New York|
    |   Julian|   Lennon|   Liverpool|
    |   Johnny|    Clegg|Johannesburg|
    +---------+---------+------------+
    



```python
# Split the data between the United Kindgom, the United States and Other Countries
df1 = dfSingers.filter("Cityname in ('Liverpool','London')")
df2 = dfSingers.filter("Cityname in ('Memphis','New York')")
df3 = dfSingers.subtract(df1).subtract(df2)

# apply conditional rules
df1 = df1.withColumn("Country",lit("United Kingdom"))
df2 = df2.withColumn("Country",lit("United States"))
df3 = df3.withColumn("Country",lit("Others"))

# union the results
df4 = df1.unionAll(df2).unionAll(df3)
df4.show()
```

    +---------+---------+------------+--------------+
    |Firstname| Lastname|    Cityname|       Country|
    +---------+---------+------------+--------------+
    |     John|   Lennon|   Liverpool|United Kingdom|
    |     Paul|McCartney|   Liverpool|United Kingdom|
    |     John|    Lydon|      London|United Kingdom|
    |   Julian|   Lennon|   Liverpool|United Kingdom|
    |    Elvis|  Presley|     Memphis| United States|
    |     Sean|   Lennon|    New York| United States|
    |   Johnny|    Clegg|Johannesburg|        Others|
    +---------+---------+------------+--------------+
    



```python
# You can also do it with when/otherwise
# Often, when rules are complicated, split/union is clearer because you can use multiple statements
from pyspark.sql.functions import when
df4 = dfSingers.withColumn("Country", \
          when(col("Cityname").isin('Liverpool','London'),lit("United Kingdom")) \
         .when(col("Cityname").isin('Memphis','New York'),lit("United States")) \
         .otherwise("Others"))

df4.show()
```

    +---------+---------+------------+--------------+
    |Firstname| Lastname|    Cityname|       Country|
    +---------+---------+------------+--------------+
    |    Elvis|  Presley|     Memphis| United States|
    |     John|   Lennon|   Liverpool|United Kingdom|
    |     Paul|McCartney|   Liverpool|United Kingdom|
    |     John|    Lydon|      London|United Kingdom|
    |     Sean|   Lennon|    New York| United States|
    |   Julian|   Lennon|   Liverpool|United Kingdom|
    |   Johnny|    Clegg|Johannesburg|        Others|
    +---------+---------+------------+--------------+
    
