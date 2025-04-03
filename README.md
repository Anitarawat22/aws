1. ** Creating the S3 Bucket**
Created an S3 bucket named athena-demoanita.

Inside the bucket, created two folders:

athenainput/ – For storing input files.

athenaresultanita/ – For storing query results.

2. **Uploading Data**
Uploaded a 57.4MB CSV file into the athenainput/ folder.

3. **Setting Up AWS Athena**
Navigated to AWS Athena and opened the Query Editor.

**Created a database named demo using the following query:**

sql
Copy
Edit
CREATE DATABASE demo;
4. **Creating the Table**
Created a table named students in the demo database, with the following schema:

sql
Copy
Edit
CREATE EXTERNAL TABLE demo.students (
    student_id INT,
    exam_center_id INT,
    subject STRING,
    year INT,
    quarter INT,
    score INT,
    grade STRING
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES (
    'skip.header.line.count' = '1'  -- Skips the header row
)
LOCATION 's3://athena-demoanita/athenainput/';
5.** Querying the Data**
Saved the table configuration and previewed the data using:

sql
Copy
Edit
SELECT * FROM demo.students LIMIT 10;
so it is sacnning the whole day 

**To optimize this**

we will be changes the file format to parquert it will skip the unnessary columns
and creating a partition and it will skip the unnessary rows

we will be coverting the csv file to parquet format
and use msck repair 
and this will scan only the data you have mentoined in the query editor.
