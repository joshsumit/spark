# spark


er1 = spark.read.csv("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
er1.rdd.saveAsTextFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC2.csv")

if  container is external put container@sparkserver / path
er1 = spark.read.csv("wasb://testcontainer@testsparksa.blob.core.windows.net/sample.csv")
er1.rdd.saveAsTextFile('wasb://testcontainer@testsparksa.blob.core.windows.net/sample2.csv')
