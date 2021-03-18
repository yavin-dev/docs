---
layout: guide
group: guide
title: Release Notes
toc: true
---

# Release 1.0.0-beta.1
{:.beta}

### New Features
#### Column Config Reordering & Sorting

- [yavin-dev/framework#1280](https://github.com/yavin-dev/framework/pull/1280) Reordering and sorting columns directly in the column config.

<img src="/assets/images/Release_demo_reordering_sorting.gif">

#### Denali Theme Support

- [yavin-dev/framework#1268](https://github.com/yavin-dev/framework/pull/1268) Support for static theming via [Denali](http://denali.design).

<img src="/assets/images/Release_denali_theme1.png" width="783px">

<img src="/assets/images/Release_denali_theme2.png" width="390px"> <img src="/assets/images/Release_denali_theme3.png" width="390px">

### <img src="/assets/images/Release_updates_icon.png" alt="updates logo" style="height: 40px; margin-bottom: -8px"> Updates & Additions

- [yahoo/elide#1897](https://github.com/yahoo/elide/pull/1897) The Aggregation Store now supports filters on metrics that have not been requested/projected in the client request.
- [yavin-dev/app#7](https://github.com/yavin-dev/app/pull/7) We now pull all supported drivers for the different dialects. This includes **Hive**, **PrestoDB**, **Druid**, **MySQL**, **Postgres**.
- [yavin-dev/framework#1291](https://github.com/yavin-dev/framework/pull/1291) The dimension selector for filter values is now sorted.
- [yavin-dev/framework#1276](https://github.com/yavin-dev/framework/pull/1276) Refactor visualization toggle to denali.
- [yavin-dev/framework#1266](https://github.com/yavin-dev/framework/pull/1266) Dashboard Header style changes.

### <img src="/assets/images/Release_bug_icon.png" alt="bug fixes logo" style="height: 40px; margin-bottom: -8px"> Bug Fixes

- [yavin-dev/framework#1285](https://github.com/yavin-dev/framework/pull/1285) Fixed a bug where searching for elide enums returned undefined.
