---
layout: guide
group: guide
title: Connect to & Model Your Data
---

{:toc}

### How do I get the demo app running on my machine using the default semantic model provided?

Check the [Quick Start Guide](https://yavin.dev/pages/guide/02-start.html)

For sample demos that comes with Yavin (we are using the [Netflix Movie and TV Shows](https://www.kaggle.com/shivamb/netflix-shows) dataset that is sourced from [Kaggle](https://www.kaggle.com/) :

[Sample DB connection config](https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/demo-configs/db/sql/DemoConnection.hjson)

[Sample default semantic model config](https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/demo-configs/models/tables/DemoTables.hjson)

### How do I connect to a new database?

Create/reuse the Hjson file for defining your data connection, example: ```DemoConnection.hjson``` in path ```yavin/packages/webservice/app/src/main/resources/demo-configs/db/sql/``` ***(Note: Multiple data connection can exist in a single Hjson file)***.

**Sample H2 Connection config:**

```
{
  dbconfigs: [
    {
      name: DemoH2Connection
      url: jdbc:h2:mem:DemoDB;DB_CLOSE_DELAY=-1;
      driver: org.h2.Driver
      user: guest
      dialect: H2
    }
  ]
}

```

**Sample Presto Connection Config :**  

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

Direct upload of CSV to Yavin is not supported for Analytic Queries. ***You can upload the CSV to a database as a table and then create a Hjson config and access it via Yavin.*** After uploading the CSV file to HDFS and creating a Hive table on it. In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/db/sql/```. Create/reuse the Hjson file to point to the CSV file using Hive, example: ```CSV_Data_connection.hjson```

**Sample Hive Connection config:**
```
{
  dbconfigs: [
    {
      name: CSV_Data_connection
      url: jdbc:hive:mem:DemoDB;DB_CLOSE_DELAY=-1;
      driver: org.hive.Driver
      user: guest
      dialect: Hive
    }
  ]
}

```

**If the CSV file you have is intended to be use alone**, then a similar approach to the demo CSV data provided by Yavin can be followed. Put a CSV file in path ```yavin/packages/webservice/app/src/main/resources/```. And in path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/db/sql/```. Create/reuse the Hjson file to point to the CSV file using H2. And in path ```yavin/packages/webservice/app/src/main/resources/demo-configs/models/tables/``` Create/reuse the Hjson file for your model configuration.

[Sample DB connection config](https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/demo-configs/db/sql/DemoConnection.hjson)

[Sample default semantic model config](https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/demo-configs/models/tables/DemoTables.hjson)

**If the CSV file is not used alone** then it has to be joined with fact data then it has to reside in the same database.

More information can be obtained at : [https://elide.io/pages/guide/v5/04-analytics.html#data-source-configuration](https://elide.io/pages/guide/v5/04-analytics.html#data-source-configuration)

### How do I create a single/multiple tables using a data connection/Database?

Create/reuse the Hjson file for your model configuration, example: ```DemoTables.hjson``` in path ```yavin/packages/webservice/app/src/main/resources/demo-configs/models/tables/``` ***(Note: Multiple model configuration can exist in a single Hjson file)***.

**Sample Hjson for two different tables :**

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

In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/models/tables/```, sharing the same file and block as tables, define your measures.

**Sample Hjson for two different measures :**

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

In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/models/tables/```, sharing the same file and block as tables, define your dimensions

**Sample Hjson for two different dimensions:**

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

### How do I define Type Ahead Search?

When constructing filters in the Yavin UI, the search bar can be used to perform ***type ahead*** queries in order to suggest dimension values.  Type ahead search can be enabled for any dimension of type `TEXT` in one of two ways.   The first is to add a `values` attribute to the dimension with a list of all possible values.  This works well when your dataset does not have a dedicated dimension table and when the set of dimension values is small:

```
{
  name : countryCode
  friendlyName : Country ISO Code
  type : TEXT
  definition : '{{playerCountry.isoCode}}'
  values : ['US', 'HK']
}
```

When your dataset does have a dedicated dimension table, you can specify an alternate semantic model that can be searched for values by adding the `tableSource` attribute.

```
{
  name: countryName
  type: TEXT
  definition: '{{playerCountry.name}}'
  tableSource: country.name
}
```

The attribute `tableSource` is a '.' separated expression consisting of two components: the table to search, followed by the column name to search in that table.  The Yavin UI will issue separate search queries against this table when the user types in the search bar.  The `tableSource` attribute can be configured to point to a different table or the same table where the dimension is defined. When neither `values` or `tableSource` is specified, Yavin will search against the selected **fact** semantic model. **Note:** If your **fact** table is very large, the type ahead queries may be slow.

### How do I join tables together in my semantic config?

In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/models/tables/```, sharing the same file and block as tables, define your joins.

**Sample Hjson for a left, right and full joins:**

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

If you want to UNION the data from two or more tables and present as a single unified table to the user, you can provide a SQL subquery in the Hjson config.

In path : ```yavin/packages/webservice/app/src/main/resources/demo-configs/models/tables/```, sharing the same file and block as tables, define your union

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

For more information on SQL definition please check out: [https://elide.io/pages/guide/v5/04-analytics.html#column-properties](https://elide.io/pages/guide/v5/04-analytics.html#column-properties)

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

If you want to filter the data available from the table to the users, you can provide a SQL subquery in the Hjson config.

**Sample Hjson for filtering on multiple fields:**

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

For more information on time grains please check out: [https://elide.io/pages/guide/v5/04-analytics.html#time-dimensions--time-grains](https://elide.io/pages/guide/v5/04-analytics.html#time-dimensions--time-grains)

### How can i share my semantic config with others?

You can upload your application code to any source code management software like Github, etc. and share with others.

Similar to the one we have for the demo app and data set:

[Sample DB connection config](https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/demo-configs/db/sql/DemoConnection.hjson)

[Sample default semantic model config](https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/demo-configs/models/tables/DemoTables.hjson)
