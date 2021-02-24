---
layout: guide
group: guide
title: How to Guide
---

### how do I get the demo app running on my machine?

Check the [Quick Start Guide](https://yavin.dev/pages/guide/02-start.html)

### how do I connect to a new database?

In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/db/sql/```

Create an Hjson file, example: ```DemoConnection.hjson```

Sample demo of an H2 connection :
```
{
  dbconfigs: [
    {
      name: DemoH2Connection
      url: jdbc:h2:mem:DemoDB;  DB_CLOSE_DELAY=-1;
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
      name: DemoPrestoDBConnection
      url: presto://PrestoDemo:8080/hive/demo; 
      driver: com.facebook.presto.jdbc.PrestoDriver
      user: MrUser
      dialect: PrestoDB
    }
  ]
}

```
More information can be obtained at : [https://elide.io/pages/guide/v5/04-analytics.html#data-source-configuration](https://elide.io/pages/guide/v5/04-analytics.html#data-source-configuration)


### how do I add a CSV file to Yavin?


### how do I connect to a new table within a dataset?


### how do I add measures in my semantic config


### how do I add dimensions in my semantic config?


### how do I join tables together in my semantic config?


### how do I union tables together in my semantic config?


### How to i convert data of one type into another type in my semantic config?


### how do I create fields like i would with a case statement in SQL in my semantic config?


### how do I filter on multiple fields like i would with SQL in my semantic config?


### How often do i need to create a new table?


### how do I add another Time Grain in my semantic config?


### How can i share my semantic config with others?
