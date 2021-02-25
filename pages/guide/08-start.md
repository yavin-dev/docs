---
layout: guide
group: guide
title: How to Semantic Model Guide
---

{:toc}

### How do I get the demo app running on my machine using the default semantic model provided?

Check the [Quick Start Guide](https://yavin.dev/pages/guide/02-start.html)

For the sample demos that comes with Yavin (we are using the [Netflix Movie and TV Shows](https://www.kaggle.com/shivamb/netflix-shows) dataset that is sourced from [Kaggle](https://www.kaggle.com/) :

[The DB connection config](https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/demo-configs/db/sql/DemoConnection.hjson)
[The default semantic model config](https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/demo-configs/models/tables/DemoTables.hjson)

### How do I connect to a new database?

In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/db/sql/```

Create an Hjson file for each data connection, example: ```DemoConnection.hjson```. You will need 1 file per connection.

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

### How do I add a CSV file to Yavin?

Direct upload of CSV to Yavin is not supported for Analytic Queries. You can upload the CSV to a database as a table and then create a Hjson config and access it via Yavin.

After uploading the CSV file to HDFS and creating a table on it. In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/db/sql/```

Create an Hjson file to point to the CSV file using Hive, example: ```CSV_Data_connection.hjson```

Sample demo of an H2 connection :
```
{
  dbconfigs: [
    {
      name: CSV_Data_connection
      url: jdbc:hive:mem:DemoDB;  DB_CLOSE_DELAY=-1;
      driver: org.hive.Driver
      user: guest
      dialect: Hive
    }
  ]
}

```

More information can be obtained at : [https://elide.io/pages/guide/v5/04-analytics.html#data-source-configuration](https://elide.io/pages/guide/v5/04-analytics.html#data-source-configuration)

### How do I create a single/multiple tables using a data connection/Database?

By defining a model configuration as described in path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/models/tables/```

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

For more information on model configuration, check [https://elide.io/pages/guide/v5/04-analytics.html#model-configuration](https://elide.io/pages/guide/v5/04-analytics.html#model-configuration)

### How do I add measures in my semantic config

In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/models/tables/```, sharing the same file as tables, define your measures.

Within the same block and file as the table that was defined, example: ```DemoTables.hjson```, define your measures

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

For more information on measures configuration, check [https://elide.io/pages/guide/v5/04-analytics.html#columns](https://elide.io/pages/guide/v5/04-analytics.html#columns)

### How do I add dimensions in my semantic config?

In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/models/tables/```, sharing the same file as tables, define your dimensions.

Within the same block and file as the table that was defined, example: ```DemoTables.hjson```, define your dimensions

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

For more information on dimensions configuration, check [https://elide.io/pages/guide/v5/04-analytics.html#columns](https://elide.io/pages/guide/v5/04-analytics.html#columns)

### How do I join tables together in my semantic config?

In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/models/tables/```, sharing the same file as tables, define your joins.

Within the same block as the table that was defined, example: ```DemoTables.hjson```, define your dimensions

Sample Hjson for a left, right and full joins:

```
joins: [
    {
       name: playerCountry
       to: country
       kind: toOne
       type: left
       definition: '{{country_id}} = {{playerCountry.id}}'
    },
    {
       name: coachState
       to: country
       kind: toOne
       type: right
       definition: '{{state_id}} = {{coachState.id}}'
    },
    {
       name: playerTeam
       to: team
       kind: toMany
       type: full
       definition: '{{team_id}} = {{playerTeam.id}}'
    }
]

```

For more information on joins, please check out: [https://elide.io/pages/guide/v5/04-analytics.html#joins](https://elide.io/pages/guide/v5/04-analytics.html#joins)

### How do I union tables together in my semantic config?

If you want to UNION the data from 2 or more tables and present as a single unified table to the user, you can provide a SQL subquery in the Hjson config.

```
{
  tables: [{
      name: PlayerStats
      sql: '''
      select name, game_type, created_on, highScore from playerStatsPractice UNION ALL select name, game_type, created_on, highScore from playerStatsChampionship
      '''
      dbConnectionName: Presto Data Source
      friendlyName: Player Stats
      description:
      '''
      A long description
      '''
      category: Sports
      cardinality : large
      readAccess : '(user AND member) OR (admin.user AND NOT guest user)'
      isFact : true
      tags: ['Game', 'Player']
      measures : [
          {
          name : highScore
          type : INTEGER
          definition: 'MAX({{highScore}})'
          friendlyName: High Score
          }
      ]
      dimensions : [
          {
              name : name
              type : TEXT
              definition : '{{name}}'
              cardinality : large
          },
          {
              name : gameType
              type : TEXT
              definition : '{{game_type}}'
              friendlyName: Game Type
          },
          {
              name : createdOn
              type : TIME
              definition : '{{created_on}}'
              grain:
              {
                  type :  DAY
                  sql :  '''PARSEDATETIME(FORMATDATETIME({{}}, 'yyyy-MM-dd'), 'yyyy-MM-dd')'''
              }
          }
      ]
  }]
}
```

For more information on subqueries please check out: [https://elide.io/pages/guide/v5/04-analytics.html#table-properties](https://elide.io/pages/guide/v5/04-analytics.html#table-properties)

### How to i convert data of one type into another type in my semantic config?

If you want to convert data from one type to another, you can provide a SQL definition for the column in the Hjson config. See below for an example of converting a Timestamp to String in 'YYYY-MM-DD' format.

```
{
    name : createdOn
    type : TEXT
    definition : '''
    FORMATDATETIME({{created_on}},'yyyy-MM-dd')
    '''
}
```

For more information on SQL definition please check out: [https://elide.io/pages/guide/v5/04-analytics.html#analytic-queries](https://elide.io/pages/guide/v5/04-analytics.html#analytic-queries)

### how do I create fields like i would with a case statement in SQL in my semantic config?

You can use CASE statement in the SQL definition for a column.    

```
{
    name : gameType
    type : TEXT
    definition : '''
    CASE WHEN {{game_type}} = 'tournament' THEN 'CHAMPIONPSHIP' ELSE {{game_type}} END
    '''
    friendlyName: Game Type
}
```

For more information on case statements please check out: [https://elide.io/pages/guide/v5/04-analytics.html#column-properties](https://elide.io/pages/guide/v5/04-analytics.html#column-properties)

### How do I filter on multiple fields like i would with SQL in my semantic config?

To filter in a field in the semantic model, you will need to use the Elide filtering operators [https://elide.io/pages/guide/v5/11-graphql.html#filtering](https://elide.io/pages/guide/v5/11-graphql.html#filtering)

If you want to filter the data available from the table to the users, you can provide a SQL subquery in the Hjson config.

Sample Hjson for filtering on multiple fields:

```
{
  tables: [{
      name: PlayerStats
      sql: '''
      select name, game_type, created_on, highScore from playerStats where highScore > 100
      '''
      dbConnectionName: Presto Data Source
      friendlyName: Player Stats
      description:
      '''
      A long description
      '''
      category: Sports
      cardinality : large
      readAccess : '(user AND member) OR (admin.user AND NOT guest user)'
      isFact : true
      tags: ['Game', 'Player']
      measures : [
          {
          name : highScore
          type : INTEGER
          definition: 'MAX({{highScore}})'
          friendlyName: High Score
          }
      ]
      dimensions : [
          {
              name : name
              type : TEXT
              definition : '{{name}}'
              cardinality : large
          },
          {
              name : gameType
              type : TEXT
              definition : '{{game_type}}'
              friendlyName: Game Type
          },
          {
              name : createdOn
              type : TIME
              definition : '{{created_on}}'
              grain:
              {
                  type :  DAY
                  sql :  '''
                  PARSEDATETIME(FORMATDATETIME({{}}, 'yyyy-MM-dd'), 'yyyy-MM-dd')
                  '''
              }
          }
      ]
  }]
}
```

For more information on subqueries please check out: [https://elide.io/pages/guide/v5/04-analytics.html#table-properties](https://elide.io/pages/guide/v5/04-analytics.html#table-properties)

### How often do i need to create a new table?

It totally depends on the use case. You can split a single Physical Table into multiple Logical Tables in Yavin with each table limited to certain type of data. On the other side, you can UNION multiple Physical tables to a single Logic Table in Yavin.

### How do I add another Time Grain in my semantic config?

To add another time grain in a date dimension, we can simply do the following:

```
    Dimensions: [
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

For more information on subqueries please check out: [https://elide.io/pages/guide/v5/04-analytics.html#time-dimensions--time-grains](https://elide.io/pages/guide/v5/04-analytics.html#time-dimensions--time-grains)

### How can i share my semantic config with others?

You can upload your application code to any source code management software like Github, etc. and share with others.

Similar to the one we have for the demo app and data set:

[The DB connection config](https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/demo-configs/db/sql/DemoConnection.hjson)
[The default semantic model config](https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/demo-configs/models/tables/DemoTables.hjson)
