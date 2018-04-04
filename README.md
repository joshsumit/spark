# spark


er1 = spark.read.csv("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
er1.rdd.saveAsTextFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC2.csv")

if  container is external put container@sparkserver / path
er1 = spark.read.csv("wasb://testcontainer@testsparksa.blob.core.windows.net/sample.csv")
er1.rdd.saveAsTextFile('wasb://testcontainer@testsparksa.blob.core.windows.net/sample2.csv')



/LOAD
val df = spark.read.json("/pathtojsonfile.json")
df.show
df.registerTempTable("sample")
df.createOrReplaceTempView("sample")

//TABLE AND SQL
spark.table("pandas")
spark.sql("select name from sample").show

//UDF
spark.udf.register("addone",(x:Int)=>x+1)

//CREATE DATASET
val ds = spark.createDataset(List(1,2,3)) 
val rdd = sc.parallelize(List(1,2,3))
val ds = spark.createDataset(rdd)



//CREATE DATAFRAME
case class Num(x:Int)
val rdd = sc.parallelize(List(Num(1),Num(2),Num(3)))
spark.createDataFrame(rdd).show

import org.apache.spark.sql.types.{StructType,StructField,IntegerType};
import org.apache.spark.sql.Row
val rowRDD = rdd.map(x=>Row(x))
val schema = StructType(Array(StructField("num", IntegerType, true)))
spark.createDataFrame(rowRDD,schema).show


//CATALOG
spark.catalog.cacheTable("pandas") // caches the table into memory, throws Table or view  not found in database exeception if not found.
spark.catalog.uncacheTable("pandas")  // to remove table from memory
spark.catalog.currentDatabase
spark.catalog.isCached("pandas")
spark.catalog.clearCache 
spark.catalog.listDatabases.take(1)
spark.catalog.listTables("default").take(1)
spark.catalog.dropTempView("pandas") //drops the table
