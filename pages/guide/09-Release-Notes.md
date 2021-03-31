---
layout: guide
group: guide
title: Release Notes
toc: true
---

# Release [2.0.0-beta.2](https://github.com/yavin-dev/app/releases/tag/v1.0.0-beta.2)
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

You can upgrade your Yavin app version to `2.0.0-beta.2` with the following commands:
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
