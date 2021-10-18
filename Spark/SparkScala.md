Spark using Scala
------------

flatMap() : invokes individually for each element in the input RDD. Produce multiple output elements 
*********************
scala> val lines = sc.parallelize(List("hello world","hi"))
lines: org.apache.spark.rdd.RDD[String] = ParallelCollectionRDD[40] at parallelize at <console>:19

scala> val words = lines.flatMap(line => line.split(" "))
words: org.apache.spark.rdd.RDD[String] = FlatMappedRDD[41] at flatMap at <console>:21

scala> words.first
res38: String = hello
 val rdd1  = sc.parallelize(List("scala","spark","hadoop","haloop"))

rdd2: org.apache.spark.rdd.RDD[String] = MappedRDD[3] at map at <console>:19
scala> println(rdd2.collect().mkString(","))
O/P :  SCALA,SPARK,HADOOP,HALOOP
scala> val rdd2 = rdd1.map(x => x.concat(x.toUpperCase()))
rdd2: org.apache.spark.rdd.RDD[String] = MappedRDD[3] at map at <console>:19
scala> rdd2.take(3).foreach(println)
	
scala> val rdd3 = rdd1.filter(x => x.contains("scala"))
rdd3: org.apache.spark.rdd.RDD[String] = FilteredRDD[4] at filter at <console>:19

scala> val numericRDD = sc.parallelize(List(1,2,3,3))
numericRDD: org.apache.spark.rdd.RDD[Int] = ParallelCollectionRDD[5] at parallelize at <console
scala> val numRDDMap = numericRDD.map(x => x+2)
numRDDMap: org.apache.spark.rdd.RDD[Int] = MappedRDD[6] at map at <console>:19

scala> numRDDMap.collect().foreach(println)
3 4 5 5	

scala> val numRddDist = numericRDD.distinct()
numRddDist: org.apache.spark.rdd.RDD[Int] = MappedRDD[11] at distinct at <console>:19
scala> numRddDist.collect().foreach(println)
1 2 3
scala> val otherRdd = sc.parallelize(List(3,4,5,6))
otherRdd: org.apache.spark.rdd.RDD[Int] = ParallelCollectionRDD[12] at parallelize at <console>:17

scala> val unionRdd = otherRdd.union(numericRDD)
unionRdd: org.apache.spark.rdd.RDD[Int] = UnionRDD[13] at union at <console>:21

scala> unionRdd.collect().foreach(println)
3 4  5 6 1 2 3 3

scala> unionRdd.countByValue.foreach(println)

scala> val inputRdd2 = sc.parallelize(List(1,2,3,3))
inputRdd2: org.apache.spark.rdd.RDD[Int] = ParallelCollectionRDD[11] at p

scala> inputRdd2.countByValue()
res6: scala.collection.Map[Int,Long] = Map(2 -> 1, 1 -> 1, 3 -> 2)

scala> inputRdd2.reduce((x,y) => x+y)
res12: Int = 9

Paired RDDs 
***********

//Create RDD
val TRDD = sc.parallelize(List("982120003,France","982120002,Germany","982120000,UnitedStates","982120001,Australia"))
//Create Paired RDD
val PairedData=TRDD.map{record => (record.split(",")(0).toLong,record.split(",")(1))}
//apply sortByKey transformation
PairedData.sortByKey(true,numPartitions=1).foreach(println)
//Create RDD
val TelecomRDD = sc.parallelize(List("982120003,John","982120002,Sam","982120000,Keny","982120001,Raj"))
//Create RDD
val IRoamingRDD = sc.parallelize(List("982120003,France","982120002,Germany","982120000,UnitedStates","982120001,Australia"))
//Create Paired RDD
val TelecomPairedData = TelecomRDD.map{record => (record.split(",")(0).toLong,record.split(",")(1))}
//Create Paired RDD
val RoamingPairedData=IRoamingRDD.map{record => (record.split(",")(0).toLong,record.split(",")(1))}
//join two RDDs based on the same key
TelecomPairedData.join(RoamingPairedData).foreach(println)

  mapValues()
***************
locationAllownace = List( loc1, 30% , loc2 , 23%)
GradeAllownace = 

//Create Scores RDD
val ScoresRDD = sc.parallelize(List("Maths,70","Science,75","English,65"))
//create paired RDD
val PairedRDD = ScoresRDD.map{record => (record.split(",")(0),record.split(",")(1).toInt)}
//apply mapValues transformaton to increment score value by 5
PairedRDD.mapValues(score => score + 5).foreach(println)
******************

scala> val rdd5 = sc.textFile("sparkdata/pairdata.txt")
rdd5: org.apache.spark.rdd.RDD[String] = /home/manju_trng/sparkdata/newpair.txt MapPartitionsRDD[38] at textFile at <console>:24

scala> rdd5.collect
res28: Array[String] = Array(1000       ETA     PUN     MANJU, 2000     ENG     TVM  JEENA, 3000      DNA     BBSR    MEENA, 4000     DNA     HYD     MEERA, 5000     ENG  TVM      JEENA, 6000     FAC     BBSR    MEENA)

scala> val rdd6 = rdd5.map(lines => lines.split("\t"))
rdd6: org.apache.spark.rdd.RDD[Array[String]] = MapPartitionsRDD[39] at map at <console>:28

scala> rdd6.collect
res29: Array[Array[String]] = Array(Array(1000, ETA, PUN, MANJU), Array(2000, ENG, TVM, JEENA), Array(3000, DNA, BBSR, MEENA), Array(4000, DNA, HYD, MEERA), Array(5000, ENG, TVM, JEENA), Array(6000, FAC, BBSR, MEENA))

scala> val unitEmpPair = rdd5.map(x => (x.split("\t")(1),x.split("\t")(0)))
unitEmpPair: org.apache.spark.rdd.RDD[(String, String)] = MapPartitionsRDD[40] at map at <console>:26

val empNoNamePair = rdd7.map(x => (x.split(",")(0),x.split(",")(3)))

scala> unitEmpPair.collect
res30: Array[(String, String)] = Array((ETA,1000), (ENG,2000), (DNA,3000), (DNA,4000), (ENG,5000), (FAC,6000))

scala> unitEmpPair.countByKey()
res31: scala.collection.Map[String,Long] = Map(ENG -> 2, FAC -> 1, ETA -> 1, DNA -> 2)

scala> val rdd6 = unitEmpPair.gropuByKey()
<console>:28: error: value gropuByKey is not a member of org.apache.spark.rdd.RDD[(String, String)]
       val rdd6 = unitEmpPair.gropuByKey()
                              ^

scala> val rdd6 = unitEmpPair.groupByKey()
rdd6: org.apache.spark.rdd.RDD[(String, Iterable[String])] = ShuffledRDD[43] at groupByKey at <console>:28

scala> rdd6.collect
res32: Array[(String, Iterable[String])] = Array((ENG,CompactBuffer(2000, 5000)), (FAC,CompactBuffer(6000)), (ETA,CompactBuffer(1000)), (DNA,CompactBuffer(3000, 4000)))

scala> val rdd7 = unitEmpPair.sortByKey()
rdd7: org.apache.spark.rdd.RDD[(String, String)] = ShuffledRDD[46] at sortByKey at <console>:28

scala> rdd7.collect.foreach(println)
(DNA,3000)
(DNA,4000)
(ENG,2000)
(ENG,5000)
(ETA,1000)
(FAC,6000)

scala> val locNamePair = rdd5.map(x => (x.split("\t")(2),x.split("\t")(3)))
locNamePair: org.apache.spark.rdd.RDD[(String, String)] = MapPartitionsRDD[47] at map at <console>:26

scala> locNamePair.collect
res34: Array[(String, String)] = Array((PUN,MANJU), (TVM,JEENA), (BBSR,MEENA), (HYD,MEERA), (TVM,JEENA), (BBSR,MEENA))


scala> val rdd5 = sc.textFile("/home/manju_trng/sparkdata/newpair.txt")
rdd5: org.apache.spark.rdd.RDD[String] = /home/manju_trng/sparkdata/newpair.txt MapPartitionsRDD[38] at textFile at <console>:24

scala> rdd5.collect
res28: Array[String] = Array(1000       ETA     PUN     MANJU, 2000     ENG     TVM  JEENA, 3000      DNA     BBSR    MEENA, 4000     DNA     HYD     MEERA, 5000     ENG  TVM      JEENA, 6000     FAC     BBSR    MEENA)

scala> val rdd6 = rdd5.map(lines => lines.split("\t"))
rdd6: org.apache.spark.rdd.RDD[Array[String]] = MapPartitionsRDD[39] at map at <console>:28

scala> rdd6.collect
res29: Array[Array[String]] = Array(Array(1000, ETA, PUN, MANJU), Array(2000, ENG, TVM, JEENA), Array(3000, DNA, BBSR, MEENA), Array(4000, DNA, HYD, MEERA), Array(5000, ENG, TVM, JEENA), Array(6000, FAC, BBSR, MEENA))
scala> val inputRdd2 = sc.parallelize(List(1,2,3,3))
inputRdd2: org.apache.spark.rdd.RDD[Int] = ParallelCollectionRDD[11] at p

scala> inputRdd2.countByValue()
res6: scala.collection.Map[Int,Long] = Map(2 -> 1, 1 -> 1, 3 -> 2)

scala> inputRdd2.reduce((x,y) => x+y)
res12: Int = 9

scala> val unitEmpPair = rdd5.map(x => (x(1),x(0)))
unitEmpPair: org.apache.spark.rdd.RDD[(String, String)] = MapPartitionsRDD[40] at map at <console>:26

scala> unitEmpPair.collect
res30: Array[(String, String)] = Array((ETA,1000), (ENG,2000), (DNA,3000), (DNA,4000), (ENG,5000), (FAC,6000))

scala> unitEmpPair.countByKey()
res31: scala.collection.Map[String,Long] = Map(ENG -> 2, FAC -> 1, ETA -> 1, DNA -> 2)

scala> val rdd6 = unitEmpPair.gropuByKey()
<console>:28: error: value gropuByKey is not a member of org.apache.spark.rdd.RDD[(String, String)]
       val rdd6 = unitEmpPair.gropuByKey()
                              ^

scala> val rdd6 = unitEmpPair.groupByKey()
rdd6: org.apache.spark.rdd.RDD[(String, Iterable[String])] = ShuffledRDD[43] at groupByKey at <console>:28

scala> rdd6.collect
res32: Array[(String, Iterable[String])] = Array((ENG,CompactBuffer(2000, 5000)), (FAC,CompactBuffer(6000)), (ETA,CompactBuffer(1000)), (DNA,CompactBuffer(3000, 4000)))

scala> val rdd7 = unitEmpPair.sortByKey()
rdd7: org.apache.spark.rdd.RDD[(String, String)] = ShuffledRDD[46] at sortByKey at <console>:28

scala> rdd7.collect.foreach(println)
(DNA,3000)
(DNA,4000)
(ENG,2000)
(ENG,5000)
(ETA,1000)
(FAC,6000)

scala> val locNamePair = rdd5.map(x => (x.split("\t")(2),x.split("\t")(3)))
locNamePair: org.apache.spark.rdd.RDD[(String, String)] = MapPartitionsRDD[47] at map at <console>:26

scala> locNamePair.collect
res34: Array[(String, String)] = Array((PUN,MANJU), (TVM,JEENA), (BBSR,MEENA), (HYD,MEERA), (TVM,JEENA), (BBSR,MEENA))

scala> locNamePair.groupByKey()
res35: org.apache.spark.rdd.RDD[(String, Iterable[String])] = ShuffledRDD[48] at groupByKey at <console>:29

scala> val broadcastVar = sc.broadcast(Array(1, 2, 3))
broadcastVar: org.apache.spark.broadcast.Broadcast[Array[Int]] = Broadcast(43)

scala> broadcastVar.value
res36: Array[Int] = Array(1, 2, 3)

scala> val v1 = Array("AAA","BBB","CCC")
v1: Array[String] = Array(AAA, BBB, CCC)

scala> val bCVar = sc.broadcast(v1)
bCVar: org.apache.spark.broadcast.Broadcast[Array[String]] = Broadcast(44)

scala> bCVar.value
res38: Array[String] = Array(AAA, BBB, CCC)

scala> val accum = sc.longAccumulator("My Accumulator")
accum: org.apache.spark.util.LongAccumulator = LongAccumulator(id: 6050, name: Some(My Accumulator), value: 0)

scala> accum.value
res39: Long = 0

scala> sc.parallelize(Array(1, 2, 3, 4)).foreach(x => accum.add(x))

scala> val acRdd = sc.parallelize(Array(1, 2, 3, 4)).foreach(x => accum.add(x))
acRdd: Unit = ()

scala> accum.value
res41: Long = 20

scala> accum.add(100)

scala> accum.value
res43: Long = 120

Spark - Scala Word Count Demo
****************************

import org.apache.spark.SparkContext
import org.apache.spark.SparkContext._
import org.apache.spark.SparkConf

object SimpleApp {
 def main(args: Array[String]) {
   val logFile = “D:/ApacheSPARK/exercises/spark/README.md"
   val conf = new SparkConf().setAppName("Simple Application")
   val sc = new SparkContext(conf)
   val logData = sc.textFile(logFile, 2).cache()
   val numAs = logData.filter(line => line.contains("a")).count()
   val numBs = logData.filter(line => line.contains("b")).count()
     println("Lines with a: %s, Lines with b: %s".format(numAs, numBs))
 }
}



