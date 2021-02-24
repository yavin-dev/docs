---
layout: guide
group: guide
title: How to Guide
---

### How do i get the demo app running on my machine?

Check the [Quick Start Guide](https://yavin.dev/pages/guide/02-start.html)

### How do i connect to a new database?

In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/db/sql/```

Create an hjson file, example: ```DemoConnection.hjson```

Sample demo of an H2 connection :
```
{
  dbconfigs: [
    {
      # We created the connection for the demo using H2 connection
      name: DemoConnection
      url: jdbc:h2:mem:DemoDB;  DB_CLOSE_DELAY=-1;  INIT=RUNSCRIPT FROM 'classpath:create-demo-data.sql'
      driver: org.h2.Driver
      user: guest
      dialect: H2
    }
  ]
}

```
Sample demo of a Presto connection :  
```
{
  dbconfigs: [
    {
      name: PrestoXT
      url: jdbc:presto://xandartan-presto.tan.ygrid.yahoo.com:4443?SSL=true&SSLCertificatePath=/Users/pdougherty16/.athenz/griduser.uid.pdougherty16.cert.pem&SSLKeyStorePath=/Users/pdougherty16/.athenz/griduser.uid.pdougherty16.key.pem&SSLTrustStorePath=/Users/pdougherty16/.athenz/yahoo_certificate_bundle.pem&SessionProperties=distributed_join=false,query_max_execution_time=30m
      driver: com.facebook.presto.jdbc.PrestoDriver
      user: MrUser
      dialect: PrestoDB
    }
  ]
}

```
More information can be obtained at : [https://elide.io/pages/guide/v5/04-analytics.html#data-source-configuration](https://elide.io/pages/guide/v5/04-analytics.html#data-source-configuration)


### How do i add a CSV file to Yavin?


### How do i connect to a new table within a dataset?


### How do i add measures in my semantic config


### How do i add dimensions in my semantic config?


### How do i join tables together in my semantic config?


### How do i union tables together in my semantic config?


### How to i convert data of one type into another type in my semantic config?


### How do i create fields like i would with a case statement in SQL in my semantic config?


### How do i filter on multiple fields like i would with SQL in my semantic config?


### How often do i need to create a new table?


### How do i add another Time Grain in my semantic config?


### How can i share my semantic config with others?
