Readme

Part 1 Database Setup for TPC-DS
Workshop Spark 


Get the TPC-DS to Postgres locally on macOs
Clone the repository

```
git clone https://github.com/gregrahn/tpcds-kit.git 
cd tpcds-kit/tools 
make OS=MACOS
```

Generate the data and create a database
```
createdb tpcds 
psql tpcds -f tpcds.sql
```

Generate data
```
./dsdgen -FORCE -VERBOSE
```
Run this script on your terminal 

```
for i in `ls *.dat`; do
  table=${i/.dat/}
  echo "Loading $table..."
  sed 's/|$//' $i > /tmp/$i
  psql tpcds -q -c "TRUNCATE $table"
  psql tpcds -c "\\copy $table FROM '/tmp/$i' CSV DELIMITER '|'"
done
```
Download Postico to check if the database is properly setup. If you installed postgres using brew use the following command to check if the postgres user is created 
```
/usr/local/opt/postgres/bin/createuser -s postgres
```