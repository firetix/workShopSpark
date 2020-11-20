Readme

# Part 1 Apache Spark - Optimization workshop
https://mohamed-rachidi.medium.com/part-1-database-setup-for-tpc-ds-e4a684731bed
## Database Setup for TPC-DS

- Clone the repository TPC-DS repository and setup the make file 

```
git clone https://github.com/gregrahn/tpcds-kit.git 
cd tpcds-kit/tools 
make OS=MACOS
```
- Generate the data and create a database
```
createdb tpcds 
psql tpcds -f tpcds.sql
```
- Generate data, Note: Change Scale to size of dataset desired. default 20 GB
```
./dsdgen -FORCE -VERBOSE -SCALE 20
```

# Notes 

This will create *.dat files similar to csv files, you can use an app like postico to get the column name and use them to read the CSV with spark in Part2.
Download Postico to check if the database is properly setup. Use the following command to check if the postgres user is created

```
/usr/local/opt/postgres/bin/createuser -s postgres
```



# Part 2 Apache Spark — Optimization workshop
https://mohamed-rachidi.medium.com/part-2-setup-jupyter-notebook-and-spark-with-scala-locally-9d46a9423ba0

## Let’s setup a standalone spark cluster
* Install jdk8 if you already have it installed check the version.

```
brew tap adoptopenjdk/openjdk
brew cask install adoptopenjdk8
```
- Check that your java version is correct

```
$java -version java version 
"1.8.0_121" Java(TM) SE Runtime Environment (build 1.8.0_121-b13) Java HotSpot(TM) 64-Bit Server VM (build 25.121-b13, mixed mode)
```

- Install scala and spark

```
brew install apache-spark
brew install scala
```
- Launch the spark cluster
```
cd /usr/local/Cellar/apache-spark/3.0.1/libexec/sbin
./start-all.sh
```

##  Second Let’s setup pyspark to run with the spark cluster

- Install jupyter, pyspark and other dependencies
```
pip install jupyter
pip install pyspark
pip install py4j
pip install pandas
```
- Setup Pysark to use jupyter instead of a terminal shell by setting the following environment variable in ~/.bashrc or ~/.zshrc or fish

```
export PYSPARK_DRIVER_PYTHON=jupyter
export PYSPARK_DRIVER_PYTHON_OPTS=notebook
```

- Clone the repository and start pyspark

```
git clone https://github.com/firetix/workShopSpark.git
cd workSHopSpark
pyspark --packages org.postgresql:postgresql:42.2.18 --master spark://localhost:7077 --conf spark.executor.instances=20 --conf spark.executor.cores=2 --conf spark.executor.memory=4g --conf spark.driver.memory=3g
```

- This setup is specific to my local machine change the following variables to match yours :
```
spark.executor.memory=
spark.executor.instances=
spark.executor.cores=
spark.driver.memory=
```
