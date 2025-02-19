influxdb-java
=============

A pure Java library to access the REST API of a InfluxDB database.

This implementation is meant as a Java rewrite of the influxdb-go package.
All low level REST Api calls are available.

Typical usage looks like:

```java
InfluxDB influxDB = InfluxDBFactory.connect("http://172.17.0.2:8086", "root", "root");

this.influxDB.createDatabase("aTimeSeries", 1);

Serie serie = new Serie("testSeries");
serie.setColumns(new String[] { "value1", "value2" });
Object[] point = new Object[] { System.currentTimeMillis(), 5 };
serie.setPoints(new Object[][] { point });
Serie[] series = new Serie[] { serie };
this.influxDB.write(dbName, series, TimeUnit.MILLISECONDS);

```

For additional usage examples have a look ad [InfluxDBTest.java](https://github.com/majst01/influxdb-java/blob/master/src/test/java/org/influxdb/InfluxDBTest.java "InfluxDBTest.java")

### Build Requirements

* Java 1.6+
* Maven 3.0+
* Docker daemon running

Maven will run tests during build process using a docker image with influxdb actual image is majst01/influxdb-java.
This docker image is pulled during the first test run which will take some time. So the first test execution will fail because the image to pull is not there.
You can check with:

```
    $ docker images | grep majst01
majst01/influxdb-java      latest              50256afac0c9        About an hour ago   298.7 MB

```

Then you can build influxdb-java with all tests with:

    $ mvn clean install

If you don't have Docker running locally, you can skip tests with -DskipTests flag set to true:

    $ mvn clean install -DskipTests=true



### TODO

Publish to maven-repo.
