---
layout: guide
group: guide
title: Release Notes
toc: true
---

# Release [1.0.0-beta.1](https://github.com/yavin-dev/app/releases/tag/v1.0.0-beta.1)
{:.beta}

### <i class="d-icon d-new-star"></i> New Features
#### Column Config Reordering & Sorting

- [yavin-dev/framework#1280](https://github.com/yavin-dev/framework/pull/1280) Reordering and sorting columns directly in the column config.

<img src="/assets/images/Release_demo_reordering_sorting.gif">

#### Denali Theme Support

- [yavin-dev/framework#1268](https://github.com/yavin-dev/framework/pull/1268) Support for static theming via [Denali](http://denali.design).

> You can try out the theme below by updating
> - `ui/app/styles/app.scss` to import `'yavin-dark-theme'` instead of `'yavin-light-theme'`
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

### <i class="d-icon d-refresh"></i> Updates & Additions

- [yavin-dev/app#7](https://github.com/yavin-dev/app/pull/7) Yavin now bundles in jdbc drivers for the all supported dialects. This includes **Hive**, **PrestoDB**, **Druid**, **MySQL**, **Postgres**.
- [yavin-dev/framework#1291](https://github.com/yavin-dev/framework/pull/1291) The dimension selector for filter values is now sorted.
- [yavin-dev/framework#1276](https://github.com/yavin-dev/framework/pull/1276) Refactor visualization toggle to denali.
- [yavin-dev/framework#1266](https://github.com/yavin-dev/framework/pull/1266) Dashboard Header style changes.

For a complete list of API changes, check out the latest [Elide Change LOG](https://github.com/yahoo/elide/blob/master/changelog.md)

### <i class="d-icon d-bug"></i> Bug Fixes

- [yavin-dev/framework#1285](https://github.com/yavin-dev/framework/pull/1285) Fixed a bug where searching for elide enums returned undefined.


## How to upgrade to a new release

- You can upgrade your Yavin app version with the following commands :
  ```shell
  cd app
  git pull origin
  ```
