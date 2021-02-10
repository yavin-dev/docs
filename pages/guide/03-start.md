---
layout: guide
group: guide
title: Setup and Installation Guide
---

## Browser Support
By default, the Yavin UI supports the most recent versions of the following browsers:
- Chrome
- Firefox
- Safari
- IE 11  

This may be customized via the app's `config/targets.js` file. More information on this file can be found [here](https://guides.emberjs.com/release/configuring-ember/build-targets/).

## Database Support

Elide analytic APIs **generate SQL queries** against your target database(s). Elide must be **configured with a Dialect** to correctly generate native SQL that matches the database grammar. Elide supports the following dialects by default:

* H2
* Hive
* Presto
* Druid
* MySQL
* Postgres

More information on dialects and how to use them can be found [here](https://elide.io/pages/guide/v5/04-analytics.html#dialects).

Semantic Models
------------------------------------------
A ***semantic model*** is the view of the data you want your users to understand.  It is typically non-relational (for simplicity) and consists of concepts like tables, measures, and dimensions.  End users refer to these concepts by name only (they are not expected to derive formulas or know about the physical storage or serialization of data).

A ***virtual semantic layer*** maps a semantic model to columns and tables in a physical database.  Yavin leverages Elide's virtual semantic layer which accomplishes this mapping through a HJSON configuration language.  [HJSON](https://hjson.github.io/) is a human friendly adaptation of JSON that allows comments and a relaxed syntax among other features.  Elide's virtual semantic layer includes the following information:

 - The defintions of tables, measures, and dimensions you want to expose to the end user.
 - Metadata like descriptions, categories, and tags that better describe and label the semantic model.
 - For every table, measure, and dimension, a SQL fragment that maps it to the physical data.  These fragements are used by elide to generate native SQL queries against the target database.

More information on Elide's analytic query support and virtual semantic layer can be found [here](https://elide.io/pages/guide/v5/04-analytics.html#overview).

### Writing your first semantic model

Elide provides its own [guide](https://elide.io/pages/guide/v5/01-start.html) for getting started that includes setting up a simle semantic model.  The following sections will illustrate how Yavin is configured to explore [Netflix movie and TV show titles](https://www.kaggle.com/shivamb/netflix-shows).

### Connections, Tables, Dimensions, Measures and Joins
When running locally, Yavin will leverage the H2 in-memory database.  The [connection configuration][demo-connection] looks like:

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

### User Interface Metadata

The Yavin UI is metadata driven and will present your semantic model:

<figure>
  <img src="/assets/images/SAI_Model_in_UI.png" width="200" />
  <figcaption>Column Selector</figcaption>
</figure>

### Type Ahead Search

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

The attribute `tableSource` is a '.' separated expression consisting of two components: the table to search, followed by the column name to search in that table.  The Yavin UI will issue separate search queries against this table when the user types in the search bar.  The `tableSource` attribute can be configured to point to a different table or the same table where the dimension is defined.

When neither `values` or `tableSource` is specified, Yavin will search against the selected **fact** semantic model. **Note:** If your **fact** table is very large, the type ahead queries may be slow.

Yavin Example Key Elements
-----------------------------------------------
The Yavin example project consists of the following key elements :

1. [HJSON configuration][demo-connection] for a H2 in-memory database.
1. [HJSON configuration][demo-table] for a table (and its respective measures and dimensions).
1. [A liquibase script][liquibase-script] that sets up your database with relevant tables needed for Yavin.
1. [Test data][test-data] that is initialized in the database.
1. [Example integration tests][integration-test] that verify the Yavin APIs are working correctly.
1. [A Spring boot application configuration file][spring-boot-config] that configures web service routes and other service level controls.

Yavin Detailed Installation Guide
-----------------------------------------------
Here are the complete steps for installing and setting up **Yavin** with your **dataset** and your **semantic models**:

### Step 1.  Install Yavin Source.

This step was covered in [quick start guide](/pages/guide/02-start.html).  Upon installation, you will have the **Yavin** repo on your local machine.  Your repo will include the following key subdirectories:

|      Path                      |  Purpose                       |
|---------------------------------|---------------------------------------|
| ```yavin/packages/webservice/app/src/main/resources/demo-configs/db/sql``` | Your dialect connection can reside here        |
| ```yavin/packages/webservice/app/src/main/resources/demo-configs/models/tables```  | Your semantic models can reside here       |
| ```yavin/packages/webservice/app/src/main/resources/application.yaml``` | The spring boot configuration file for your application |
| ```yavin/packages/webservice/app/src/main/kotlin/com/yahoo/yavin/ws/filters``` | Directory for web request filters including authentication |
| ```yavin/packages/webservice/app/src/main/resources/db/changelog/changelog.xml``` | Database changelog for setting up the database |
{:.table}

### Step 2.  Setup Your Database.

Yavin requires a database to store user information, reports, dashboards, and other application objects.  The **Yavin** repo includes a [liquibase-script][liquibase-script] for creating these tables.  The script may require modifications to work with your target database.

### Step 3.  Configure the Database Connection.

Add a database configuration file to connect to your database.  More information about database configuration files can be found [here](https://elide.io/pages/guide/v5/04-analytics.html#data-source-configuration).

### Step 4.  Define your Semantic Model.

Add one or more semantic model definition files.  More information about adding tables can be found [here](https://elide.io/pages/guide/v5/04-analytics.html#model-configuration).

### Step 5.  Secure your Semantic Model.

Yavin allows you to limit access to tables, measures, and dimensions by user role.  There are three steps involved:

1.  Create a security roles file which enumerates the roles your application will have.  More information can be found [here](https://elide.io/pages/guide/v5/04-analytics.html#security-configuration).
2.  Update your semantic model, by adding `readAccess` rules for tables, measures, and dimensions you want to restrict.  These rules can include a single role or a complex security expression with multiple roles joined by logical AND (conjunction), OR (disjunction), and parenthetic groupings.
3.  Yavin stores users and roles in two separate database tables (`user` and `roles`).  The roles table must be updated to include all the roles defined in step 1.  When a user is added to the database, it must be assigned 1 or more roles.

Yavin also supports row level security.  Row level security requires building your application with custom `FilterExpressionCheck` classes.  These classes have names that can be leveraged in `readAccess` rules similar to roles.  More information on custom security checks can be found [here](https://elide.io/pages/guide/v5/03-security.html#filter-expression-checks).

### Step 6.  Define an authentication filter for the application.

Yavin comes bundled with an [example filter][auth-filter] that authenticates every user as admin.  You will want to replace this example with a servlet filter that authenticates your users.

### Step 7.  Configure Your Application

Yavin is a spring boot application.  The default configuration can be found [here][spring-boot-config].  This configuration allows you to change a number of settings including:
 - The application port.
 - The routes for the APIs.
 - Location of liquibase migration scripts (if you run them as part of application boot).

The configuration file has sections including:
 1. [Spring Boot configuration](https://docs.spring.io/spring-boot/docs/current/reference/html/appendix-application-properties.html)
 2. [Elide configuration](https://elide.io)

The application configuration supports profiles for enabling different settings for different environments.

### Step 8.  Build Your Application

To build Yavin as a jar, run the following command:
```
cd packages/webservice && ./gradlew bootJar
```

### Step 9.  Validate Semantic Model

The build creates a fat jar with all dependencies including a tool that can be leveraged to validate your semantic model before deploying or running your service.
More details about validating the semantic model can be found [here](https://elide.io/pages/guide/v5/04-analytics.html#configuration-validation).

### Step 10.  Run Your Application

To run Yavin locally, simple execute:
```
cd packages/webservice && ./gradlew bootRun
```

### Step 11.  Launch the Application
Launch Yavin on your browser by loading [http://localhost:8080](http://localhost:8080).

[demo-connection]: https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/demo-configs/db/sql/DemoConnection.hjson
[demo-table]: https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/demo-configs/models/tables/DemoTables.hjson
[liquibase-script]: https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/db/changelog/changelog.xml
[test-data]: https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/netflix_titles.csv
[integration-test]: https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/test/kotlin/com/yahoo/yavin/ws/test/integration/DemoDataSourceTest.kt
[spring-boot-config]: https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/resources/application.yaml
[auth-filter]: https://github.com/yahoo/yavin/blob/master/packages/webservice/app/src/main/kotlin/com/yahoo/yavin/ws/filters/AuthFilter.kt
