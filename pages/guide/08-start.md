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


### how do I create a single/multiple tables using a data connection/Database?

In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/models/tables/```

Create an Hjson file, example: ```DemoTables.hjson```

Sample Hjson for 2 tables :

```
{
  tables: [
    {
      name:  Table1
      friendlyName: My Table 1
      table: My_Table_1
      dbConnectionName: DemoH2Connection
    }
    {
      name:  Table2
      friendlyName: My Table 2
      table: My_Table_2
      dbConnectionName: DemoPrestoDBConnection
    }      
}

```

### how do I add measures in my semantic config

In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/models/tables/```, sharing the same file as tables, define your measures.

Within the same block as the table that was defined, example: ```DemoTables.hjson```, define your measures

Sample Hjson for 2 measures :

```
      measures: [
        {
          # A count measure
          name: measure1
          friendlyName: Measure 1
          category: MeasureCategory1
          type: INTEGER
          definition: 'count({{title_id}})'
        }
        {
          # A measure using a sum and a condition
          name: measure2
          friendlyName: Measure 2
          category: Stats
          type: INTEGER
          definition: "sum(cast (case when {{duration}} like '% Seasons' then REPLACE({{duration}}, ' Seasons', '') else '0' end AS INT))"
        }
        ...
      ]

```

### how do I add dimensions in my semantic config?

In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/models/tables/```, sharing the same file as tables, define your dimensions.

Within the same block as the table that was defined, example: ```DemoTables.hjson```, define your dimensions

Sample Hjson for 2 dimensions:

```
    Dimensions: [
      {
        # A simple straight forward dimension. Mapping to a field in the schema
        name: dimension1
        friendlyName: Dimension 1
        category: DimCategory1
        type: TEXT
        definition: '{{title_id}}'
      }
      {
        # A Date Dimension using multiple time grains (year and day)
        name: dimension2
        friendlyName: Dimension 2
        category: DimCategory2
        type: TIME
        definition: '{{release_year}}'
        grains: [
          {
             type: YEAR
          }
          {
             type: DAY
          }
        ]
      }
        ...
    ]

```


### how do I join tables together in my semantic config?


### how do I union tables together in my semantic config?


### How to i convert data of one type into another type in my semantic config?


### how do I create fields like i would with a case statement in SQL in my semantic config?


### how do I filter on multiple fields like i would with SQL in my semantic config?


### How often do i need to create a new table?


### how do I add another Time Grain in my semantic config?


### How can i share my semantic config with others?
