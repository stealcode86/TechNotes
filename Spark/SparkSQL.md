SparkSQL using Scala
---------

Creating Data Frames

SQLContext or SparkSession

scala> val df = spark.read.json("sparkdata/people.json")

df: org.apache.spark.sql.DataFrame = [age: bigint, name: string]

scala> df.show() +----+-------+ | age| name| +----+-------+ |null|Michael| | 30| Andy| | 19| Justin| | 20| Sandy| | 19| Jeffin| | 50| Mandy| | 29| Kevin| | 45| Ash| | 59| Josh| +----+-------+

scala> df.printSchema root |-- age: long (nullable = true) |-- name: string (nullable = true)

scala> df.select("name").show +-------+ | name| +-------+ |Michael| | Andy| | Justin| | Sandy| | Jeffin| | Mandy| | Kevin| | Ash| | Josh| +-------+

scala> df.select($"name",$"age"+10).show +-------+----------+ | name|(age + 10)| +-------+----------+ |Michael| null| | Andy| 40| | Justin| 29| | Sandy| 30| | Jeffin| 29| | Mandy| 60| | Kevin| 39| | Ash| 55| | Josh| 69| +-------+----------+

scala> df.select("name","age").show +-------+----+ | name| age| +-------+----+ |Michael|null| | Andy| 30| | Justin| 19| | Sandy| 20| | Jeffin| 19| | Mandy| 50| | Kevin| 29| | Ash| 45| | Josh| 59| +-------+----+

scala> df.filter($"age" > 21).show() +---+-----+ |age| name| +---+-----+ | 30| Andy| | 50|Mandy| | 29|Kevin| | 45| Ash| | 59| Josh| +---+-----+

scala> df.groupBy("age").count().show() +----+-----+ | age|count| +----+-----+ | 29| 1| | 19| 2| | 50| 1| |null| 1| | 59| 1| | 30| 1| | 20| 1| | 45| 1| +----+-----+

scala> df.createOrReplaceTempView("people")

scala> spark.sql("select * from people").show +----+-------+ | age| name| +----+-------+ |null|Michael| | 30| Andy| | 19| Justin| | 20| Sandy| | 19| Jeffin| | 50| Mandy| | 29| Kevin| | 45| Ash| | 59| Josh| +----+-------+

scala> spark.sql("select * from people where name like 'A%'").show +---+----+ |age|name| +---+----+ | 30|Andy| +---+----+

scala> spark.sql("select * from people where name like 'J%'").show +---+------+ |age| name| +---+------+ | 19|Justin| | 19|Jeffin| +---+------+

val irisCSV = spark.read.format("csv").option("sep", ",").option("inferSchema", "true").option("header", "true").load("PySparkData/iris/iris.csv")

scala> case class IrisClass(Sepal_Length:Double, Sepal_Width:Double, Petal_Length:Double, Petal_Width:Double, Species:String) defined class IrisClass

val irisDF1 = irisRDD.filter(c => c!=header).map(_.split(",")).map(c => IrisClass(c(0).toDouble,c(1).toDouble,c(2).toDouble, c(3).toDouble, c(4))).toDF("Sepal_Length", "Sepal_Width", "Petal_Length", "Petal_Width", "Species") scala> case class IrisClass(Sepal_Length:Double, Sepal_Width:Double, Petal_Length:Double, Petal_Width:Double, Species:String) defined class IrisClass

scala> val irisDF1 = irisRDD.filter(c => c!=header).map(_.split(",")).map(c => IrisClass(c(0).toDouble,c(1).toDouble,c(2).toDouble, c(3).toDouble, c(4))).toDF("Sepal_Length", "Sepal_Width", "Petal_Length", "Petal_Width", "Species") irisDF1: org.apache.spark.sql.DataFrame = [Sepal_Length: double, Sepal_Width: double ... 3 more fields]

scala> irisDF1.printSchema root |-- Sepal_Length: double (nullable = false) |-- Sepal_Width: double (nullable = false) |-- Petal_Length: double (nullable = false) |-- Petal_Width: double (nullable = false) |-- Species: string (nullable = true)

scala> irisDF1.show +------------+-----------+------------+-----------+-------+ |Sepal_Length|Sepal_Width|Petal_Length|Petal_Width|Species| +------------+-----------+------------+-----------+-------+ | 5.1| 3.5| 1.4| 0.2| setosa| | 4.9| 3.0| 1.4| 0.2| setosa| | 4.7| 3.2| 1.3| 0.2| setosa| | 4.6| 3.1| 1.5| 0.2| setosa| | 5.0| 3.6| 1.4| 0.2| setosa| | 5.4| 3.9| 1.7| 0.4| setosa| | 4.6| 3.4| 1.4| 0.3| setosa| | 5.0| 3.4| 1.5| 0.2| setosa| | 4.4| 2.9| 1.4| 0.2| setosa| | 4.9| 3.1| 1.5| 0.1| setosa| | 5.4| 3.7| 1.5| 0.2| setosa| | 4.8| 3.4| 1.6| 0.2| setosa| | 4.8| 3.0| 1.4| 0.1| setosa| | 4.3| 3.0| 1.1| 0.1| setosa| | 5.8| 4.0| 1.2| 0.2| setosa| | 5.7| 4.4| 1.5| 0.4| setosa| | 5.4| 3.9| 1.3| 0.4| setosa| | 5.1| 3.5| 1.4| 0.3| setosa| | 5.7| 3.8| 1.7| 0.3| setosa| | 5.1| 3.8| 1.5| 0.3| setosa| +------------+-----------+------------+-----------+-------+ only showing top 20 rows

scala> val irisDF1 = irisRDD.filter(c => c!=header).map(_.split(",")).map(c => IrisClass(c(0).toDouble,c(1).toDouble,c(2).toDouble, c(3).toDouble, c(4))).toDF("Sepal_Length", "Sepal_Width", "Petal_Length", "Petal_Width", "Species") irisDF1: org.apache.spark.sql.DataFrame = [Sepal_Length: double, Sepal_Width: double ... 3 more fields]

scala> irisDF1.createOrReplaceTempView("iristab")

scala> spark.sql("select * from iristab").show +------------+-----------+------------+-----------+-------+ |Sepal_Length|Sepal_Width|Petal_Length|Petal_Width|Species| +------------+-----------+------------+-----------+-------+ | 5.1| 3.5| 1.4| 0.2| setosa| | 4.9| 3.0| 1.4| 0.2| setosa| | 4.7| 3.2| 1.3| 0.2| setosa| | 4.6| 3.1| 1.5| 0.2| setosa| | 5.0| 3.6| 1.4| 0.2| setosa| | 5.4| 3.9| 1.7| 0.4| setosa| | 4.6| 3.4| 1.4| 0.3| setosa| | 5.0| 3.4| 1.5| 0.2| setosa| | 4.4| 2.9| 1.4| 0.2| setosa| | 4.9| 3.1| 1.5| 0.1| setosa| | 5.4| 3.7| 1.5| 0.2| setosa| | 4.8| 3.4| 1.6| 0.2| setosa| | 4.8| 3.0| 1.4| 0.1| setosa| | 4.3| 3.0| 1.1| 0.1| setosa| | 5.8| 4.0| 1.2| 0.2| setosa| | 5.7| 4.4| 1.5| 0.4| setosa| | 5.4| 3.9| 1.3| 0.4| setosa| | 5.1| 3.5| 1.4| 0.3| setosa| | 5.7| 3.8| 1.7| 0.3| setosa| | 5.1| 3.8| 1.5| 0.3| setosa| +------------+-----------+------------+-----------+-------+ only showing top 20 rows

irisDF1.createOrReplaceTempView("iristab")

scala> irisCSV.printSchema root |-- Sepal_Length: double (nullable = true) |-- Sepal_Width: double (nullable = true) |-- Petal_Length: double (nullable = true) |-- Petal_Width: double (nullable = true) |-- Species: string (nullable = true)

scala> irisCSV.show +------------+-----------+------------+-----------+-------+ |Sepal_Length|Sepal_Width|Petal_Length|Petal_Width|Species| +------------+-----------+------------+-----------+-------+ | 5.1| 3.5| 1.4| 0.2| setosa| | 4.9| 3.0| 1.4| 0.2| setosa| | 4.7| 3.2| 1.3| 0.2| setosa| | 4.6| 3.1| 1.5| 0.2| setosa| | 5.0| 3.6| 1.4| 0.2| setosa| | 5.4| 3.9| 1.7| 0.4| setosa| | 4.6| 3.4| 1.4| 0.3| setosa| | 5.0| 3.4| 1.5| 0.2| setosa| | 4.4| 2.9| 1.4| 0.2| setosa| | 4.9| 3.1| 1.5| 0.1| setosa| | 5.4| 3.7| 1.5| 0.2| setosa| | 4.8| 3.4| 1.6| 0.2| setosa| | 4.8| 3.0| 1.4| 0.1| setosa| | 4.3| 3.0| 1.1| 0.1| setosa| | 5.8| 4.0| 1.2| 0.2| setosa| | 5.7| 4.4| 1.5| 0.4| setosa| | 5.4| 3.9| 1.3| 0.4| setosa| | 5.1| 3.5| 1.4| 0.3| setosa| | 5.7| 3.8| 1.7| 0.3| setosa| | 5.1| 3.8| 1.5| 0.3| setosa| +------------+-----------+------------+-----------+-------+ only showing top 20 rows

/********************** Working with DataSets*******************************/

scala> case class Person(name: String, age: Long) defined class Person

scala> val caseClassDS = Seq(Person("Andy", 32),Person("Sandy",33),Person("Kandy",34)).toDS() 18/03/29 10:49:40 WARN HiveConf: HiveConf of name hive.in.default does not exist 18/03/29 10:49:41 WARN HiveConf: HiveConf of name hive.in.default does not exist 18/03/29 10:49:45 WARN HiveConf: HiveConf of name hive.in.default does not exist caseClassDS: org.apache.spark.sql.Dataset[Person] = [name: string, age: bigint]

scala> caseClassDS.show +-----+---+ | name|age| +-----+---+ | Andy| 32| |Sandy| 33| |Kandy| 34| +-----+---+

scala> caseClassDS.show +-----+---+ | name|age| +-----+---+ | Andy| 32| |Sandy| 33| |Kandy| 34| +-----+---+

scala> caseClassDS.select("name") res4: org.apache.spark.sql.DataFrame = [name: string]

scala> caseClassDS.select("name").show +-----+ | name| +-----+ | Andy| |Sandy| |Kandy| +-----+

scala> val primitiveDS = Seq(1, 2, 3).toDS() primitiveDS: org.apache.spark.sql.Dataset[Int] = [value: int]

scala> primitiveDS.map(_ + 1).collect()

scala> val path = "sparkdata/people.json" path: String = /home/manju_trng/sparkdata/people.json

scala> val peopleDS = spark.read.json(path).as[Person] peopleDS: org.apache.spark.sql.Dataset[Person] = [age: bigint, name: string]

scala> peopleDS.show +----+-------+ | age| name| +----+-------+ |null|Michael| | 30| Andy| | 19| Justin| | 20| Sandy| | 19| Jeffin| | 50| Mandy| | 29| Kevin| | 45| Ash| | 59| Josh| +----+-------+

/***************** Creating Data Frames from RDDs ********************************/

scala> case class Person(name: String, age: Long) defined class Person

scala> val personRdd1 = sc.textFile("/home/manju_trng/sparkdata/people.txt") personRdd1: org.apache.spark.rdd.RDD[String] = /home/manju_trng/sparkdata/people.txt MapPartitionsRDD[1] at textFile at :24

scala> personRdd1.collect res0: Array[String] = Array(Michael,29, Andy,30, Justin,19, AAA,78, BBB,70, CCC,75, DDD,67, EEE,44, FFF,34, GGG,23)

scala> val personRdd2 = personRdd1.map(_.split(",")) personRdd2: org.apache.spark.rdd.RDD[Array[String]] = MapPartitionsRDD[2] at map at :26

scala> personRdd2.collect res1: Array[Array[String]] = Array(Array(Michael, 29), Array(Andy, 30), Array(Justin, 19), Array(AAA, 78), Array(BBB, 70), Array(CCC, 75), Array(DDD, 67), Array(EEE, 44), Array(FFF, 34), Array(GGG, 23))

scala> val personRdd3 = personRdd2.map(attributes => Person(attributes(0), attributes(1).trim.toInt)) personRdd3: org.apache.spark.rdd.RDD[Person] = MapPartitionsRDD[3] at map at :30

scala> val peopleDF = personRdd3.toDF() 18/03/27 10:26:21 WARN HiveConf: HiveConf of name hive.in.default does not exist 18/03/27 10:26:22 WARN HiveConf: HiveConf of name hive.in.default does not exist 18/03/27 10:26:24 ERROR ObjectStore: Version information found in metastore differs 2.1.0 from expected schema version 1.2.0. Schema verififcation is disabled hive.metastore.schema.verification so setting version. 18/03/27 10:26:25 WARN HiveConf: HiveConf of name hive.in.default does not exist peopleDF: org.apache.spark.sql.DataFrame = [name: string, age: bigint]

scala> peopleDF.show +-------+---+ | name|age| +-------+---+ |Michael| 29| | Andy| 30| | Justin| 19| | AAA| 78| | BBB| 70| | CCC| 75| | DDD| 67| | EEE| 44| | FFF| 34| | GGG| 23| +-------+---+

scala> peopleDF.select("name").show() +-------+ | name| +-------+ |Michael| | Andy| | Justin| | AAA| | BBB| | CCC| | DDD| | EEE| | FFF| | GGG| +-------+

scala> peopleDF.createOrReplaceTempView("peopleview")

scala> spark.sql("SELECT name, age FROM peopleview WHERE age BETWEEN 30 AND 69") res5: org.apache.spark.sql.DataFrame = [name: string, age: bigint]

scala> spark.sql("SELECT name, age FROM peopleview WHERE age BETWEEN 30 AND 69").show +----+---+ |name|age| +----+---+ |Andy| 30| | DDD| 67| | EEE| 44| | FFF| 34| +----+---+

/*********DAY 4 ***************************Programmatic creation of DF ******************************************************/

scala> case class Person(name: String, age: Long) defined class Person

scala> val personRdd1 = sc.textFile("/home/manju_trng/sparkdata/people.txt") personRdd1: org.apache.spark.rdd.RDD[String] = /home/manju_trng/sparkdata/people.txt MapPartitionsRDD[1] at textFile at :24

scala> personRdd1.collect res0: Array[String] = Array(Michael,29, Andy,30, Justin,19, AAA,78, BBB,70, CCC,75, DDD,67, EEE,44, FFF,34, GGG,23)

scala> val personRdd2 = personRdd1.map(_.split(",")) personRdd2: org.apache.spark.rdd.RDD[Array[String]] = MapPartitionsRDD[2] at map at :26

scala> personRdd2.collect res1: Array[Array[String]] = Array(Array(Michael, 29), Array(Andy, 30), Array(Justin, 19), Array(AAA, 78), Array(BBB, 70), Array(CCC, 75), Array(DDD, 67), Array(EEE, 44), Array(FFF, 34), Array(GGG, 23))

scala> val personRdd3 = personRdd2.map(attributes => Person(attributes(0), attributes(1).trim.toInt)) personRdd3: org.apache.spark.rdd.RDD[Person] = MapPartitionsRDD[3] at map at :30

scala> val peopleDF = personRdd3.toDF() 18/03/27 10:26:21 WARN HiveConf: HiveConf of name hive.in.default does not exist 18/03/27 10:26:22 WARN HiveConf: HiveConf of name hive.in.default does not exist 18/03/27 10:26:24 ERROR ObjectStore: Version information found in metastore differs 2.1.0 from expected schema version 1.2.0. Schema verififcation is disabled hive.metastore.schema.verification so setting version. 18/03/27 10:26:25 WARN HiveConf: HiveConf of name hive.in.default does not exist peopleDF: org.apache.spark.sql.DataFrame = [name: string, age: bigint]

scala> peopleDF.show +-------+---+ | name|age| +-------+---+ |Michael| 29| | Andy| 30| | Justin| 19| | AAA| 78| | BBB| 70| | CCC| 75| | DDD| 67| | EEE| 44| | FFF| 34| | GGG| 23| +-------+---+

scala> peopleDF.select("name").show() +-------+ | name| +-------+ |Michael| | Andy| | Justin| | AAA| | BBB| | CCC| | DDD| | EEE| | FFF| | GGG| +-------+

scala> peopleDF.createOrReplaceTempView("peopleview")

scala> spark.sql("SELECT name, age FROM peopleview WHERE age BETWEEN 30 AND 69") res5: org.apache.spark.sql.DataFrame = [name: string, age: bigint]

scala> spark.sql("SELECT name, age FROM peopleview WHERE age BETWEEN 30 AND 69").show +----+---+ |name|age| +----+---+ |Andy| 30| | DDD| 67| | EEE| 44| | FFF| 34| +----+---+

scala> val peopleRDD = sc.textFile("/home/manju_trng/sparkdata/people.txt") peopleRDD: org.apache.spark.rdd.RDD[String] = /home/manju_trng/sparkdata/people.txt MapPartitionsRDD[15] at textFile at :24

scala> val schemaString = "name age" schemaString: String = name age

scala> import org.apache.spark.sql.types._ import org.apache.spark.sql.types._

scala> val fields = schemaString.split(" ").map(fieldName => StructField(fieldName, StringType, nullable = true)) fields: Array[org.apache.spark.sql.types.StructField] = Array(StructField(name,StringType,true), StructField(age,StringType,true))

scala> val schema = StructType(fields) schema: org.apache.spark.sql.types.StructType = StructType(StructField(name,StringType,true), StructField(age,StringType,true))

scala> import org.apache.spark.sql.Row import org.apache.spark.sql.Row

scala> val rowRDD = peopleRDD.map(_.split(",")).map(attributes => Row(attributes(0), attributes(1).trim)) rowRDD: org.apache.spark.rdd.RDD[org.apache.spark.sql.Row] = MapPartitionsRDD[3] at map at :30

scala> val peopleDF = spark.createDataFrame(rowRDD, schema) 18/03/30 10:38:46 WARN HiveConf: HiveConf of name hive.in.default does not exist 18/03/30 10:38:48 WARN HiveConf: HiveConf of name hive.in.default does not exist 18/03/30 10:38:51 WARN HiveConf: HiveConf of name hive.in.default does not exist peopleDF: org.apache.spark.sql.DataFrame = [name: string, age: string]

scala> peopleDF.createOrReplaceTempView("people")

scala> spark.sql("SELECT name FROM people") res2: org.apache.spark.sql.DataFrame = [name: string]

scala> spark.sql("SELECT name FROM people").show +-------+ | name| +-------+ |Michael| | Andy| | Justin| | AAA| | BBB| | CCC| | DDD| | EEE| | FFF| | GGG| +-------+

scala> peopleDF.createOrReplaceTempView("peopleview")

scala> peopleDF.show +-------+---+ | name|age| +-------+---+ |Michael| 29| | Andy| 30| | Justin| 19| | AAA| 78| | BBB| 70| | CCC| 75| | DDD| 67| | EEE| 44| | FFF| 34| | GGG| 23| +-------+---+

scala> val filterDF= spark.sql("SELECT name, age FROM peopleview WHERE age BETWEEN 30 AND 99") filterDF: org.apache.spark.sql.DataFrame = [name: string, age: bigint]

scala> filterDF.show +----+---+ |name|age| +----+---+ |Andy| 30| | AAA| 78| | BBB| 70| | CCC| 75| | DDD| 67| | EEE| 44| | FFF| 34| +----+---+

/********************** Working with hive from Spark *************************************/

$ sampledata.tx

AAA 11 BBB 12 CCC 13 DDD 14 EEE 15 FFF 16 GGG 15 HHH 14

scala> val hivedf1 = spark.sql("CREATE TABLE ManjusDB.mynewhivetable(name STRING, age INT) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' "); hivedf1: org.apache.spark.sql.DataFrame = []

scala> val hivedf2 = spark.sql("LOAD DATA LOCAL INPATH 'sampledata.txt' INTO TABLE ManjusDB.mynewhivetable") hivedf2: org.apache.spark.sql.DataFrame = []

scala> val hiveselect = spark.sql("select * from ManjusDB.mynewhivetable")

scala> spark.sql("select * from ManjusDB.mynewhivetable").show +----+---+ |name|age| +----+---+ | AAA| 11| | BBB| 12| | CCC| 13| | DDD| 14| | EEE| 15| | FFF| 16| | GGG| 15| | HHH| 14| +----+---+

scala> val hivedf1 = spark.sql("CREATE TABLE sparkHive(name STRING, age INT) ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' "); hivedf1: org.apache.spark.sql.DataFrame = []

scala> spark.sql("LOAD DATA LOCAL INPATH '/home/manju_trng/sparkdata/sampledata.txt' INTO TABLE sparkHive") res4: org.apache.spark.sql.DataFrame = []

scala> val hiveselect = spark.sql("select * from sparkHive") hiveselect: org.apache.spark.sql.DataFrame = [name: string, age: int]

scala> hiveselect.show +----+---+ |name|age| +----+---+ | AAA|111| | BBB| 67| | CCC|780| | DDD| 54| | EEE| 78| | FFF| 90| | GGG| 66| | HHH| 33| | III| 99| | JJJ| 11| | KKK| 77| +----+---+

****************** SaveAsTable Demo ***************************

import org.apache.spark.sql.{Row, SaveMode, SparkSession}

scala> df.write.mode(SaveMode.Overwrite).saveAsTable("ManjusDB.TemperatureTab")
