# Hive Partition

1.  Partitions are the horizontal slices of the data. It is a way of dividing a table into related parts based on the values of
    partitioned columns such as date, city, and department. 
	
2. 	Using partition, it is easy to query a portion of the data.
	
3.  Without Partitioning, Hive reads all the data in the directory and applies the query filters on it. 
    This is slow and expensive since all the data has to be read.
	
	```
	In real time we would have GB, TB and even PB of data. Suppose we have a file of 10 GB containing data of all the employees
	and their departments. Without the concept of Partitioning, the whole 10 GB file will be stored in single directory. Now 
	suppose we want to query the data of ‘Account’ department, Hive has to scan the full file and retrieve only those rows where
	department is ‘Account’. So query retrieval will take time in this case, So why not to create separate directory for each 
	department and save only that department data in it? 
	
	This can be done by partitioning that table on Department column. After Partitioning, hive will only scan Account File if account
	data is queried.
	```

4.  To apply the partitioning in Hive, we need to understand the domain of the data on which analysis needs to be done. With this knowledge,
    identification of frequently queries column and identification of column with low cardinality becomes easy and the partitioning feature 
	of hive can be applied on the selected column.	
	
## When to Use Partitioning ? 

1.  When we want data contained within a table to be split across multiple sections in Hive table.
2.  When we want to analyse only relevant subset of data, resulting in highly improved performance of Hive queries.
	
	  ```
	  Example Scenarios
      
	  Customer/user details are partitioned by country/state for fast retrieval of subset data pertaining to some category.
      Sales records are partitioned by product type, country, year and month for fast retrieval of subset data pertaining to some Product from some Country.
      Employee details are partitioned by Department for fast retrieval of subset data pertaining to some department.	
	  ```
## Types of Partitioning 

Static Partition and Dynamic Partition.	  

## Static Partition

1.  it requires the knowledge of data in beforehand

2.  we have to write separate query to load each partition. So it is advisable to use static partition where cardinality of partition
    column is very low, which will result in less number of partitions.
	
3.  While loading data, you need to specify which partition to store the data in. This means that with each load, you need to specify
    the partition column value.	

4.  If you want to use the Static partition in the hive you should set property set hive.mapred.mode = strict this property set by
    default in hive-site.xml	
	
## Dynamic Partition	

1.  It is suitable when data is unknown to us or it has more unique values in partitioning column.

2.  With dynamic partitioning in hive, partitions get created automatically at load times. New partitions can be created dynamically from existing data.

3.  Static Partitioning is faster than dynamic, as in static partitioning we provide everything at beforehand to hive, so there will be less comparisons,
    but in dynamic hive by itself has to do all the comparisons and then load the data in appropriate partition thus slower.

4.  When you have large data stored in a table then Dynamic partition is suitable

5.  If you want to partition number of column but you don’t know how many columns then also dynamic partition is suitable

6.  If you want to use the Dynamic partition in the hive you should set property set hive.mapred.mode = nonstrict 


## Pros & Cons of Partitioning

#### Pros –

1.  Distribute execution load horizontally
2.  Query response is faster as query is processed on a small datasets instead of entire datasets.

#### Cons –

1.  Having large number of partitions create number of files/ directories in HDFS, which creates overhead for NameNode as it maintains metadata.
2.  It may optimize certain queries based on where clause, but may cause slow response for queries based on grouping clause