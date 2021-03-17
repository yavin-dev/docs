---
layout: guide
group: guide
title: Release Notes
toc: true
---

# Release 1.0 BETA

## Column config reordering, sorting ability

- Ability to add column to the column config section of the report
- Ability to remove sort from column config

![](/assets/images/Release_demo_reordering_sorting.gif)


## Added support for [Denali](http://denali.design) theming

Now with only a few easy steps, we have support for Denali theming.
<img src="/assets/images/Release_denali_theme1.png">
<img src="/assets/images/Release_denali_theme2.png">
<img src="/assets/images/Release_denali_theme3.png">


## Other miscellaneous updates/additions/Bug Fixes

### <img src="/assets/images/Release_updates_icon.png" alt="updates logo" style="height: 40px; margin-bottom: -8px"> Updates & Additions

- The Aggregation Store now supports filters on metrics that have not been requested/projected in the client request. [View PR](https://github.com/yahoo/elide/commit/1c6cfbe04941b27b9de28cf04084744439c8f5e6)
- We now pull all supported drivers for the different dialects. We added support to include drivers for following dialects: **Hive**, **PrestoDB**, **Druid**, **MySQL**, **Postgres** [View PR](https://github.com/yavin-dev/app/pull/7)
- Refactor visualization toggle to denali. [View PR](https://github.com/yavin-dev/framework/pull/1276)
- Dashboard Header style changes. [View PR](https://github.com/yavin-dev/framework/pull/1266)

### <img src="/assets/images/Release_bug_icon.png" alt="bug fixes logo" style="height: 40px; margin-bottom: -8px"> Bug Fixes
- Elide enum value search. [View PR](https://github.com/yavin-dev/framework/pull/1285)
