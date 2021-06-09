---
layout: guide
group: guide
title: Release Notes
toc: true
---

# Release [1.0.0-beta.5](https://github.com/yavin-dev/app/releases/tag/v1.0.0-beta.5)
{:.beta}

### <i class="d-icon d-new-star"></i> New Features

####  Yavin App Published Builds

- [yavin-dev/app#29](https://github.com/yavin-dev/app/pull/29) Docker image support

Add custom hjson to docker container for exploring additional data sources:
  ```shell
  docker run -v <your path>:/etc/yavin -p 9999:8080 verizonmedia/yavin:latest
  ```

Launch demo app using latest yavin-app jar:
  ```shell
  curl https://raw.githubusercontent.com/yavin-dev/app/master/yavin-run.sh | bash
  ```

#### Report Builder Sidebar

- [yavin-dev/framework#1385](https://github.com/yavin-dev/framework/pull/1385) The Report Builder view now has a collapsible sidebar for selecting datasources, tables, and metrics/dimensions.

<img src="/assets/images/release_1_5_1385.gif" width="800px">

### <i class="d-icon d-dashboard"></i> Performance Changes

- [yavin-dev/framework#1382](https://github.com/yavin-dev/framework/pull/1382) Loads metadata in background and only waits if needed.

### <i class="d-icon d-activity"></i> Updates & Additions

- [yavin-dev/framework#1393](https://github.com/yavin-dev/framework/pull/1393) Adds support for suggestion columns for dimensions.

<img src="/assets/images/release_1_5_1393.png" width="400px">

- [yavin-dev/framework#1389](https://github.com/yavin-dev/framework/pull/1389) Denali Styling for table config.

<img src="/assets/images/release_1_5_1389.png" width="600px">

### Upgrade Steps

You can upgrade your Yavin app version to `1.0.0-beta.5` with the following commands:
  ```shell
  cd app
  git pull origin
  ./gradlew clean
  ```

<hr>

# Release [1.0.0-beta.4](https://github.com/yavin-dev/app/releases/tag/v1.0.0-beta.4)
{:.beta}

### <i class="d-icon d-new-star"></i> New Features

#### Data Export : Ability to export the data to CSV

- [yavin-dev/framework#1363](https://github.com/yavin-dev/framework/pull/1363) Export to CSV is now supported for reports.

<img src="/assets/images/Release_4_2.gif">


### <i class="d-icon d-activity"></i> Updates & Additions

- [yavin-dev/framework#1366](https://github.com/yavin-dev/framework/pull/1366) Added dropdown functionality to click on parameter chips and be able to change filter parameters in the filter builder.

<img src="/assets/images/Release_4_2.png" width="400px">

- [yavin-dev/app#22](https://github.com/yavin-dev/app/pull/22) With the new independent demo jar published in maven central you now have the ability to disable demo using jar dependency.

> Comment out [this line](https://github.com/yavin-dev/app/blob/a1aeef1ac1375d32ebf1c3b7c3301dad7214e91f/ws/build.gradle.kts#L23-L24) in `build.gradle.kts` to disable the demo data
> ```
> // implementation("dev.yavin","demo-config","0.9")
> ```
{:.info}

### Upgrade Steps

You can upgrade your Yavin app version to `1.0.0-beta.4` with the following commands:
  ```shell
  cd app
  git pull origin
  ./gradlew clean
  ```

<hr>

# Release [1.0.0-beta.3](https://github.com/yavin-dev/app/releases/tag/v1.0.0-beta.3)
{:.beta}

### <i class="d-icon d-activity"></i> Updates & Additions

- [yavin-dev/framework#1329](https://github.com/yavin-dev/framework/pull/1329) Update report and dashboard actions to denali.

<img src="/assets/images/Release_3_1329.png" width="725px">

### <i class="d-icon d-bug"></i> Bug Fixes

- [yavin-dev/framework#1354](https://github.com/yavin-dev/framework/pull/1354) Fix dimension select text wrapping. The dimension select assumed the height of each entry was the same which caused issues with wrapping long text.

<img src="/assets/images/Release_3_1354_before.png" width="400px"> <img src="/assets/images/Release_3_1354_after.png" width="325px">

- [yavin-dev/framework#1362](https://github.com/yavin-dev/framework/pull/1362) Columns are now only draggable by the handle. Fixes an issue where column config features such as renaming were difficult to use.
- [yavin-dev/framework#1349](https://github.com/yavin-dev/framework/pull/1349) Fixes the bug introduced by [yavin-dev/framework#1333](https://github.com/yavin-dev/framework/pull/1333) where the dimension select might not get all dimension values.


### Upgrade Steps

You can upgrade your Yavin app version to `1.0.0-beta.3` with the following commands:
  ```shell
  cd app
  git pull origin
  ./gradlew clean
  ```

<hr>

# Release [1.0.0-beta.2](https://github.com/yavin-dev/app/releases/tag/v1.0.0-beta.2)
{:.beta}

### <i class="d-icon d-activity"></i> Updates & Additions

- [yavin-dev/framework#1333](https://github.com/yavin-dev/framework/pull/1333) Use Ember concurrency for data interfaces/adapters. (Enables cancelling typeahead queries)
  > This introduced a bug in the dimension selector where it expects the elide `pageSize` in your `application.yaml` to be
  > larger that the size of `<= SMALL` cardinality dimensions.
  > ```
  > elide:
  >   pageSize: 1234
  > ```
  >
  > If this is not set, some dimensions may appear to be missing from the dropdown.
  {:.warning}

- [yavin-dev/framework#1334](https://github.com/yavin-dev/framework/pull/1334) Add week, isoweek, month grains for elide.
- [yavin-dev/framework#1335](https://github.com/yavin-dev/framework/pull/1335) Refactor column-selector.

<img src="/assets/images/Release_2_1335.png" width="200px">

- [yavin-dev/framework#1296](https://github.com/yavin-dev/framework/pull/1296) Use chips for parameters in filter builder display.

<img src="/assets/images/Release_2_1296.png">

- [yavin-dev/framework#1295](https://github.com/yavin-dev/framework/pull/1295) Allow parameters in elide filters (e.g. filtering on Year grain, but requesting Day grain)


### Upgrade Steps

You can upgrade your Yavin app version to `1.0.0-beta.2` with the following commands:
  ```shell
  cd app
  git pull origin
  ./gradlew clean
  ```

<hr>

# Release [1.0.0-beta.1](https://github.com/yavin-dev/app/releases/tag/v1.0.0-beta.1)
{:.beta}

### <i class="d-icon d-new-star"></i> New Features
#### Column Config Reordering & Sorting

- [yavin-dev/framework#1280](https://github.com/yavin-dev/framework/pull/1280) Support for reordering and sorting columns directly in the column config. You no longer need to run a request to apply sorts and can reorder columns outside of the table visualization.

<img src="/assets/images/Release_demo_reordering_sorting.gif">

#### Denali Theme Support

- [yavin-dev/framework#1268](https://github.com/yavin-dev/framework/pull/1268) Support for static theming via [Denali](http://denali.design).

> You can try out the theme below by updating
> - `ui/app/styles/app.scss` to import `'yavin-dark-theme` instead of `yavin-light-theme`
> - `ui/app/index.html` to have `<body class="denali-dark-theme">`
{:.info}

<img src="/assets/images/Release_denali_theme1.png" width="783px">

<img src="/assets/images/Release_denali_theme2.png" width="390px"> <img src="/assets/images/Release_denali_theme3.png" width="390px">


### <i class="d-icon d-dashboard"></i> Performance Changes

[yahoo/elide#1876](https://github.com/yahoo/elide/pull/1876) N+1 performance improvements in the JPA data store.  The JPA store will now return proxied collections (allowing the ORM to batch fetch the collection) and filter, sort, and paginate in memory whenever fetching a collection (N>1) of collections.  There is a feature flag to enable/disable this behavior.


### <i class="d-icon d-cloud-service"></i> API Changes

 - [yahoo/elide#1897](https://github.com/yahoo/elide/pull/1897) The Aggregation Store now supports filters on metrics that have not been requested/projected in the client request. (***Note***: This is not yet available in the Yavin UI)

> For a complete list of API changes, check out the latest [Elide Changelog](https://github.com/yahoo/elide/blob/7a11ee300605ed0130d89a036ed221d49f1b1d9c/changelog.md#500-pr32)
{:.info}

### <i class="d-icon d-activity"></i> Updates & Additions

- [yavin-dev/app#7](https://github.com/yavin-dev/app/pull/7) Jdbc drivers for supported dialects (**Hive**, **PrestoDB**, **Druid**, **MySQL**, **Postgres**) are now included by default.
- [yavin-dev/framework#1291](https://github.com/yavin-dev/framework/pull/1291) The dimension selector for filter values is now sorted.
- [yavin-dev/framework#1276](https://github.com/yavin-dev/framework/pull/1276) Refactor visualization toggle to denali.
- [yavin-dev/framework#1266](https://github.com/yavin-dev/framework/pull/1266) Dashboard Header style changes.

### <i class="d-icon d-bug"></i> Bug Fixes

- [yavin-dev/framework#1285](https://github.com/yavin-dev/framework/pull/1285) Fixed a bug where searching for elide enums returned undefined.

### Upgrade Steps

You can upgrade your Yavin app version to `1.0.0-beta.1` with the following commands:
  ```shell
  cd app
  rm -rf ui/node_modules
  git pull origin
  ```
