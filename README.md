The goals of this project are:

1. Provide a simple example of a Java application interacting with [Apache Phoenix](http://phoenix.apache.org/) & [Apache HBase](http://hbase.apache.org/) via the Phoenix JDBC driver.
2. Act as a flexible performance testing tool for a variety of read and write workloads

##Build:##

**Build for Thin JDBC Client**
```
mvn clean package
```

**Build for Thick JDBC Client**
```
mvn clean package -P thick
```

##Running Performance Tests:##

**Write Performance Test**
```
#See mixed-test.props for comments on the function of each property.
java -jar target/perf-1.0-SNAPSHOT.jar conf/write-test.props
```

Write tests include population of a table with "random" values. Modify WriteThread.java as needed to control how this dummy data is generated.

**Read Performance Test**
```
#See mixed-test.props for comments on the function of each property.
java -jar target/perf-1.0-SNAPSHOT.jar conf/read-test.props
```

**Simultaneous Read/Write Performance Test**
```
#See mixed-test.props for comments on the function of each property.
java -jar target/perf-1.0-SNAPSHOT.jar conf/mixed-test.props
```

To run a series of prep statements, put them in files under the specified setupQueryDir. You can include multiple files and multiple statements (separated by ';') in this directory.

It's also useful to define a test table schema and indices here.

**Example DDL**
```
$> cat conf/setup/test.sql
CREATE TABLE IF NOT EXISTS test(
  cust_id integer not null,
  process_id integer not null,
  doc_id integer not null,
  doc varchar,
  constraint my_pk primary key (cust_id, process_id, doc_id)
);
CREATE INDEX IF NOT EXISTS process_id_index ON test (process_id) INCLUDE(cust_id, doc_id);
```

**Example Output on a 2014 MacBook Pro:**
```

```

#ToDo:
1. More examples demonstrating differences between read/write performance for various primary key and indexing strategies
