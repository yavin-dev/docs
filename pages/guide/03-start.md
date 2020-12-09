---
layout: guide
group: guide
title: Setup and Installation Guide
---

* TOC
{:toc}

Yavin UI browser support
-------------------------------------------------
Yavin UI is an HTML-based browser application that is supported on the 3 recent versions of the following browsers:
-   ***Chrome***
-   ***Firefox***
-   ***Safari***

Overview
--------------------------------------------------------------
Before you can use Yavin to **visualize and analyze data**, you need to define your **semantic model** and database configuration in Elide. 

### Data source dialects
Elide analytic APIs **generate SQL queries** against your target database(s). Elide must be **configured with a Dialect** to correctly generate native SQL that matches the database grammar. Elide supports the following dialects by default:

* H2
* Hive
* Presto
* MySQL

More information on dialects and how to use them can be found [here](https://elide.io/pages/guide/v5/04-analytics.html#dialects). 

Semantic Models
------------------------------------------
A ***semantic model*** is the view of the data you want your users to understand.   It is typically non-relational (for simplicity) and consists of concepts like tables, measures, and dimensions.  End users refer to these concepts by name only (they are not expected to derive formulas or know about the physical storage or serialization of data).

A ***virtual semantic layer*** maps a semantic model to columns and tables in a physical database.  Yavin leverages Elide's virtual semantic layer which accomplishes this mapping through a HJSON configuration language.  [HJSON](https://hjson.github.io/) is a human friendly adaptation of JSON that allows comments and a relaxed syntax among other features.  Elide's virtual semantic layer includes the following information:
    - The defintions of tables, measures, and dimensions you want to expose to the end user.
    - Metadata like descriptions, categories, and tags that better describe and label the semantic model.
    - For every table, measure, and dimension, a SQL fragment that maps it to the physical data.  These fragements are used by elide to generate native SQL queries against the target database.

More information on Elide's analytic query support and virtual semantic layer can be found [here](https://elide.io/pages/guide/v5/04-analytics.html#overview).

### Writing your first semantic model

Elide provides its own [guide](https://elide.io/pages/guide/v5/01-start.html) for getting started that includes setting up a simle semantic model.  The following sections will illustrate how Yavin is configured to explore [Netflix movie and TV show titles](https://www.kaggle.com/shivamb/netflix-shows).

#### Connections, Tables, Dimensions, Measures and Joins
When running locally, Yavin will leverage the H2 in-memory database.  The [connection configuration][demo-connection] looks like:

```
{
  dbconfigs: [
    {
      __comment1: "We created the connection for the demo using H2 connection."
      name: DemoConnection
      url: jdbc:h2:mem:DemoDB;  DB_CLOSE_DELAY=-1;  INIT=RUNSCRIPT FROM 'classpath:create-demo-data.sql'
      driver: org.h2.Driver
      user: guest
      dialect: H2
    }
  ]
}

```

Yavin's demo data includes a single table in its [semantic model][demo-table] NetflixTitles:   


```
{
  tables: [
    {
      # The API name
      name:  NetflixTitles

      # The name presented in the UI
      friendlyName: Netflix Titles

      # The physical table where the data lives.
      table: netflix_titles

      # The database to run queries against
      dbConnectionName: DemoConnection

      # The list of dimensions
      dimensions: [
        {
          # The API name of the dimension.
          name: title_id

          # The name of the dimension presented in the UI
          friendlyName: Title Id
          category: Attributes

          # The data type
          type: TEXT

          # A templated SQL fragment that fetches this dimension.  'title_id' here is the physical database column name.
          definition: '{{title_id}}'
        }
        {
          name: show_type
          friendlyName: Show Type
          category: Attributes
          type: TEXT
          definition: '{{type}}'
        }
        {
          name: title
          friendlyName: Title
          category: Attributes
          type: TEXT
          definition: '{{title}}'
        }
        {
          name: director
          friendlyName: Director
          category: Attributes
          type: TEXT
          definition: '{{director}}'
        }
        {
          name: cast
          friendlyName: Cast List
          category: Attributes
          type: TEXT
          definition: '{{cast_list}}'
        }
        {
          name: country
          friendlyName: Countries
          category: Attributes
          type: TEXT
          definition: '{{country}}'
        }
        {
          name: date_available
          category: Date
          type: TIME
          definition: '{{date_added}}'
          grain: {
            type: DAY
          }
        }
        {
          name: release_year
          category: Date
          type: TIME
          definition: '{{release_year}}'
          grain: {
            type: YEAR
          }
        }
        {
          name: film_rating
          friendlyName: Film Rating
          category: Attributes
          type: TEXT
          definition: '{{rating}}'
        }
        {
          name: genres
          friendlyName: Genre
          category: Attributes
          type: TEXT
          definition: '{{listed_in}}'
        }
        {
          name: description
          friendlyName: Description
          category: Attributes
          type: TEXT
          definition: '{{description}}'
        }
      ]

      # The list of measures
      measures: [
        {

          # The API name of the measure.
          name: count

          # The name of measure dimension presented in the UI
          friendlyName: Title Count
          category: Stats

          # The data type
          type: INTEGER

          # A templated SQL fragment that fetches this measure.  'title_id' here is the physical database column name.
          definition: 'count({{title_id}})'
        }
        {
          name: total_seasons
          friendlyName: Total Seasons
          category: Stats
          type: INTEGER
          definition: "sum(cast (case when {{duration}} like '% Seasons' then REPLACE({{duration}}, ' Seasons', '') else '0' end AS INT))"
        }
        {
          name: movie_duration
          friendlyName: Duration (in mins)
          category: Stats
          type: INTEGER
          definition: "sum(cast (case when {{duration}} like '% min' then REPLACE({{duration}}, ' min', '') else '0' end AS INT))"
        }
      ]
    }
  ]
}
```

Note: The Netflix demo data only sourced from a single physical table.  More complex data models may source from multiple physical tables and require joins at query time.  More information about joins can be found [here](https://elide.io/pages/guide/v5/04-analytics.html#joins).

<figure><img src="assets/images/SAI_Model_in_UI.png"/>
    <figcaption>Figure - Result of the UI pulling the model (Table, Dimension, Metrics, Joins)</figcaption> 
</figure>

Yavin Example Key Elements
-----------------------------------------------
The Yavin example project consists of the following key elements :

1. [HJSON configuration][demo-connection] for a H2 in-memory database.
1. [HJSON configuration][demo-table] for a table (and its respective measures and dimensions).
1. HJSON configuration for any security roles you want defined.
1. [A liquibase script][liquibase-script] that sets up your database with relevant tables needed for Yavin.
1. [Test data][test-data] that is initialized in the database.
1. [Example integration tests][integration-tests] that verify the Yavin APIs are working correctly.
1. [A Spring boot application configuration file][spring-boot-config] that configures web service routes, security, and other service level controls.

Yavin Detailed Installation Guide
-----------------------------------------------
Here are the complete steps for installing and setting up **Yavin** with **your data-source** and your **semantic models**:
-  ***Installation***: The “<a href="">Quick Start Guide</a>” walks you through the **steps to setup Yavin** on your system with a built in "*Netflix and TV Shows*" data.
-  Upon installation (Step 1) you will have the **Yavin** repo on your local machine: <a href="https://github.com/yahoo/navi" >https://github.com/yahoo/navi/</a>.
-  Your repo will include the following key subdirectories:

|      Path                      |  Purpose                       |
|---------------------------------|---------------------------------------|
| ```navi/scripts```  | The published script of Yavin        |
| ```navi/Packages/webservice/app/src/main/resources/ ```  | Your sample data can reside here       |
| ```navi/Packages/webservice/app/src/main/resources/ ``` | Your SQL queries can reside here          |
| ```navi/Packages/webservice/app/src/main/resources/demo-configs/db/sql``` | Your dialect connection can reside here        |
| ```navi/Packages/webservice/app/src/main/resources/demo-configs/models/tables```  | Your semantic models can reside here       |
{:.table}
1.  🛑  STOP, **If your purpose is check how Yavin works using the demo app provided (Without adding any new data sources or semantic models). Then, you should be all set to Jump to step 10.**
2.  Select the correct “Data Dialect”. More information on data dialects can be found here: <a href="https://elide.io/pages/guide/v5/04-analytics.html#dialects" >https://elide.io/pages/guide/v5/04-analytics.html#dialects</a>.
3.  You must set both the “enable analytic queries” and the “Hjson configuration” feature flags. Reference: <a href="https://elide.io/pages/guide/v5/04-analytics.html#feature-flags" >https://elide.io/pages/guide/v5/04-analytics.html#feature-flags</a>.  
4.  Configure the files layout: Analytic model configuration can either be specified through JVM classes decorated with Elide annotations or Hjson configuration files. <a href="https://elide.io/pages/guide/v5/04-analytics.html#file-layout" >https://elide.io/pages/guide/v5/04-analytics.html#file-layout</a>.Path:  ../navi/Packages/
5.  Set the data source configuration for the Data Source(s) you will be using: <a href="https://elide.io/pages/guide/v5/04-analytics.html#data-source-configuration" >https://elide.io/pages/guide/v5/04-analytics.html#data-source-configuration</a>. Path on where your data source connection can reside: ../navi/Packages/webservice/app/src/main/resources/demo-configs/db/sql/
6.  Model your data. Your model may be mapped to one or more physical databases, tables, and columns and need not be a “one to one” mirror of the source semantic models. More details on this step can be found at: <a href="https://elide.io/pages/guide/v5/04-analytics.html#model-configuration" >https://elide.io/pages/guide/v5/04-analytics.html#model-configuration</a>. Path on where your semantic models can reside: ../navi/Packages/webservice/app/src/main/resources/demo-configs/models/tables
7.  Decide what roles users will need and then configure your security model as per these instructions: <a href="https://elide.io/pages/guide/v5/04-analytics.html#security-configuration" >https://elide.io/pages/guide/v5/04-analytics.html#security-configuration</a>.  
8.  To avoid having to repeat the same configuration block information multiple times, all Hjson files (table, security, and data source) support a variable substitution feature that allows a JSON structure to be associated to a variable name, and then that variable to be used in configuration files. Details can be found at:<a href="https://elide.io/pages/guide/v5/04-analytics.html#variable-substitution" >https://elide.io/pages/guide/v5/04-analytics.html#variable-substitution</a> 
9.  Before proceeding further, you should validate all of your configuration files. All of the Hjson configuration files are validated by a JSON schema. To validate you configuration, run the following command line:
10. To run Yavin, execute the following command: ```cd packages/webservice && ./gradlew```

⏱Within minutes, you will be able to launch Yavin on your local browser connection to the “Netflix movies and TV shows data source”, by launching the  following URL: <a href="http://localhost:8080">http://localhost:8080</a>

[demo-connection]: https://github.com/yahoo/navi/blob/master/packages/webservice/app/src/main/resources/demo-configs/db/sql/DemoConnection.hjson
[demo-table]: https://github.com/yahoo/navi/blob/master/packages/webservice/app/src/main/resources/demo-configs/models/tables/DemoTables.hjson
[liquibase-script]: https://github.com/yahoo/navi/blob/master/packages/webservice/app/src/main/resources/db/changelog/changelog.xml
[test-data]: https://github.com/yahoo/navi/blob/master/packages/webservice/app/src/main/resources/netflix_titles.csv
[integration-test]: https://github.com/yahoo/navi/blob/master/packages/webservice/app/src/test/kotlin/com/yahoo/navi/ws/test/integration/DemoDataSourceTest.kt
[spring-boot-config]: https://github.com/yahoo/navi/blob/master/packages/webservice/app/src/main/resources/application.yaml
