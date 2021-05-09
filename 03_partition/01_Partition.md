# Hive Partition

1.  Partitions are the horizontal slices of the data. It is a way of dividing a table into related parts based on the values of
    partitioned columns such as date, city, and department. 
	
2. 	Using partition, it is easy to query a portion of the data.
	
3.  Without Partitioning, Hive reads all the data in the directory and applies the query filters on it. 
    This is slow and expensive since all the data has to be read.
	
	```
	In real time we would have GB, TB and even PB of data. Suppose we have a file of 10 GB containing data of 
	all the employees and their departments. Without the concept of Partitioning, the whole 10 GB file will be stored 
	in single directory.Now suppose we want to query the data of ‘Account’ department, Hive has to scan the full file
	and retrieve only those rows where department is ‘Account’. So query retrieval will take time in this case, So why 
	not to create separate directory for each department and save only that department data in it? 
	This can be done by partitioning that table on Department column. 
	After Partitioning, hive will only scan Account File if account data is queried.
	```