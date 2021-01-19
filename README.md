# big-data-wrangling

# Big Data Wrangling With Google Books Ngrams
Due: Dec 06, 2020 by 11:59pm

In this assignment, you will apply the skills you've learned in the Big Data Fundamentals unit to load, filter, and visualize a large real-world dataset in cloud-based distributed computing environment using Hadoop, Spark, and the S3 filesystem.

The Google Ngrams dataset was created by Google's research team by analyzing all of the content in Google Books - these digitized texts represent approximately 4% of all books ever printed, and span a time period from the 1800s into the 2000s.

The dataset is hosted in a public S3 bucket as part of the Amazon S3 Open Data Registry. For this assignment, we have converted the data to CSV and hosted it on a public S3 bucket which may be accessed here: s3://brainstation-dsft/eng_1M_1gram.csv

For this assignment, we will follow a Big Data analysis workflow where we filter and reduce data down to a manageable size, and then do some analysis locally on our machine after extracting data from the Cloud and processing it using Big Data tools. The workflow and steps in the process are illustrated below: 

Complete the following steps below to process and analyze the data. Please document all your steps and commands/code; you may do so entirely inside of one document (e.g. a Jupyter notebook) or you may wish to split up your submission into code and written documentation (.py and .rtf, .docx, or .pdf).

Spin up a new EMR cluster using the AWS Console. Be sure to include Hadoop, Hive, Spark, and Jupyterhub for your cluster.
Connect to the head node of the cluster using SSH.
Copy the data folder from the S3 bucket into the /user/hadoop/eng_1M_1gram directory in the Hadoop file system (HDFS) using distcp. The full path for the 1-gram data directory is s3://brainstation-dsft/eng_1M_1gram.csv
Using pyspark, read the data you copied into HDFS in Step 3. You may either use Jupyterhub on EMR (the default user and password are jovyan and jupyter) or work from pyspark in the terminal if you prefer. Once you have created a pyspark DataFrame, complete the following steps below:
Show the schema of the table in pyspark
Display the total number of rows of data
Create a new DataFrame from a query using Spark SQL, filtering out only rows where the token is "data"
Get a count of the number of rows for the above.
Write the filtered data back to a directory in the Hadoop filesystem from Spark using df.write.csv() - e.g. /user/hadoop/eng_data_1gram. Be sure to pass the header=True parameter. Examine the contents of what you've written using hadoop fs -ls.
Collect the contents of the directory into a single file on the local drive of the head node using getmerge: e.g. hadoop fs -getmerge /user/hadoop/eng_data_1gram eng_data_1gram.csv. Move this file into a S3 bucket in your account using aws s3 cp.
On your local machine (or on AWS outside of Spark) in python, read the CSV data from the S3 folder into a pandas DataFrame using the fully-qualified S3 path and pd.read_csv (Note that you must have first authenticated on your machine using aws configure on the command line to complete this step). Plot the number of occurrences of the token (the frequency column) of data over the years using matplotlib.
