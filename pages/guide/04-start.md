---
layout: guide
group: guide
title: Getting Started with the UI
---

## Yavin Directory

The default landing page of Yavin is the start of your data exploration. The Directory view carries all the active reports (individual data visualizations) / Dashboards (a group of related reports) that you have previously created..

Within the Directory view you can:
- Create new Reports & Dashboards
- Filter based on your ***Favorites*** Reports & Dashboards
- Search for specific a Reports or Dashboards
- Filter by Reports or Dashboards
- Perform actions on a Report or Dashboard (Clone, Share, Delete)

<figure>
  <img src="/assets/images/GS_my_data_list.gif" width=800/>
  <figcaption>Using the Directory View</figcaption>
</figure>

### Create A New Report or Dashboard

Create a new report or dashboard by clicking on one of the following buttons:

<figure>
  <img src="/assets/images/GS_new.png" width=300/>
  <figcaption>New Report & Dashboard Buttons</figcaption>
</figure>

### Directory View Operations

From the Directory view, the following operations can be performed on saved or draft items:



|      Operation                      |  Availability                       |
|---------------------------------|---------------------------------------|
| Clone ![Clone](/assets/images/GS_clone.png) | Now |
| Export ![Export](/assets/images/GS_download.png) | Q1  2021 |
| Share ![Share](/assets/images/GS_share.png)  | Now |
| Delete ![Delete](/assets/images/GS_delete_icon.png) | Now         |
{:.table}


## Reports
A report is a user defined query coupled with a visual representation (table, graph, etc) of the returned query result. With a report, you can freely explore the various dimensions and measures of your data. Shown below is a line chart visualization from a report showing the “Netflix TV shows release dates”, filtering only for TV shows, and release date equal to 2014. With “Release Date” as dimension and “Total Seasons” and “Count” as measures.

<figure>
  <img src="/assets/images/GS_Yavin_report_in_action.gif" width="800"/>
  <figcaption>Yavin Report View</figcaption>
</figure>

### Report Operations

![](/assets/images/GS_report_action_long_list.png)

From within the report you have multiple options. Each option is shown with its associated screen icon. You can do any of the following:
You can rename, add to favorite, add to dashboard, copy API query, clone, export, share and delete.


|      Operation                  |  Availability                       |
|---------------------------------|-------------------------------------|
| Rename <img src="/assets/images/GS_edit.png" width="35"/> | Now         |
| Add to Favorite <img src="/assets/images/GS_star.png" width="35"/>      |     Now          |
| <img src="/assets/images/GS_add_to_dashboard_withText.png" width="150"/>| Now          |
| <img src="/assets/images/GS_copy_api_query_withText.png" width="150"/>| Now        |
| <img src="/assets/images/GS_clone_with_text.png" width="100"/>| Now         |
| <img src="/assets/images/GS_export_with_text.png" width="100"/>   |   Q1 2021   |
| <img src="/assets/images/GS_share_withText.png" width="100"/>   |  Now    |
| <img src="/assets/images/GS_delete.png" width="100"/>   |  Now    |
{:.table}

All operations are associated with a tooltips guide:
<figure>
  <img src="/assets/images/GS_report_action_anima.gif" width="800"/>
  <figcaption>Tooltips Are Available On All Actions</figcaption> 
</figure>

At any time in a report, you can perform one of the following operations : **Run**, **Save**, **Save As**, **Revert**
<figure>
  <img src="/assets/images/GS_report_action.png" width="400"/>
  <figcaption>Report Persistance Actions</figcaption> 
</figure>

### Exploring Reports
Reports are designed to be explored intuitively, easily and quickly.

1.  Create a new report from Yavin’s directory view <figure><img src="/assets/images/GS_my_data_new_report.png" width="100"/></figure>
1.  Select a table <figure><img src="/assets/images/GS_table_selector.png"/></figure>
1.  Select a dimension <figure><img src="/assets/images/GS_dimension_selector.png" width="250"/></figure>
1.  Select a measure <figure><img src="/assets/images/GS_metric_selector.png" width="250"/></figure>
1.  Update your filters <figure><img src="/assets/images/GS_report_filter_sample.png"/></figure>
1.  Select run report button <figure><img src="/assets/images/GS_run_saveReport.png"/></figure>

Here is a brief, animated demo showing how to explore and run a Yavin Report :
<figure> 
  <img src="/assets/images/GS_managing_reports.gif" width="800"/>
  <figcaption>Reports Demo</figcaption>
</figure>

## Dashboards
Yavin lets you take multiple reports and organize them into a dashboard, combining different visualizations. Dashboards allow you to position and size the individual reports as you desire. They are useful when your user may need to compare various reports or take multiple views of data into account.

<figure>
  <img src="/assets/images/GS_dashboard_sample.png" width="800"/>
  <figcaption>Yavin Dashboard View</figcaption> 
</figure>

From within a Dashboard, you can do all of the following. The on-screen icon is shown beside the command:

![](/assets/images/GS_dashboard_options_long_list.png)

|      Operation                      |  Availability                       |
|---------------------------------|---------------------------------------|
| Rename <img src="/assets/images/GS_edit.png" width="35"/> | Now         |
| Add to Favorite <img src="/assets/images/GS_star.png" width="35"/>|     Now          |
| <img src="/assets/images/GS_clone_with_text.png" width="100"/> | Now         |
| <img src="/assets/images/GS_share_withText.png" width="100"/>   |  Now    |
| <img src="/assets/images/GS_delete.png" width="100"/>   |  Now    |
| <img src="/assets/images/GS_add_widget.png" width="100"/> |  Now    |
| <img src="/assets/images/GS_settings_add_filter.png" width="100"/>    |  Now    |
{:.table}

At any time in a dashboard, you can perform one of the following operations : **Save Changes**, **Revert Changes**
<figure>
  <img src="/assets/images/GS_dashboard_action.png" width="250"/>
  <figcaption>Dashboard Persistance Actions</figcaption> 
</figure>

### Exploring and Managing Dashboards
Dashboards are designed for intuitive data exploration.

<figure>
  <img src="/assets/images/GS_managing_dashboard.gif" width="800"/>
  <figcaption>Exploring Dashboards Widgets</figcaption>
</figure>

Dashboards are built by adding reports to them one at a time. There are two ways of adding a report to a dashboard.
- Through the Dashboard view.
- Through the report view.

### Adding Reports To A Dashboard From The Dashboard View
From the dashboard itself, use the ***+ Add Widget*** button :

1.  Select <figure><img src="/assets/images/GS_add_widget.png" width="150"/></figure> to add an already existing report to the Dashboard
1.  Select the report like this: <figure><img src="/assets/images/GS_add_widget_dialog.png" width="400"/></figure>
1.  You can choose between creating a new report or using an existing one : <figure><img src="/assets/images/GS_add_widget2.png" width="350"/></figure> <figure><img src="/assets/images/GS_add_search_widget.png" width="350"/></figure>
1.  The Report will be added to the dashboard as a widget: <figure><img src="/assets/images/GS_table_row.png"/></figure>
1.  The Widget can be resized, edited and deleted: <figure><img src="/assets/images/GS_table_sample.png"/></figure>

### Adding Reports to a Dashboard from the Report view
1. A report can be added to the dashboard by selecting a previously saved report through the ***Add to Dashboard*** option as illustrated: <figure><img src="/assets/images/GS_dashboard_tool_tip.png" width="300"/></figure>
1. You can choose to create a new Dashboard, or to add the report to an existing dashboard: <figure><img src="/assets/images/GS_add_to_dashboard.png" width="350"/></figure> <figure><img src="/assets/images/GS_add_to_dashboard_select_widget.png" width="350"/></figure>

#### Modifying / Editing Dashboards:
The reports/widgets in a dashboard can be organized, resized, explored, filtered and edited to align with how you want the Dashboard to look. Reports in a Dashboard can be edited by clicking on the pencil icon in the header of the widget/report. This will activate the edit mode for that report. Reports in a dashboard can also be resized, re-arranged and deleted.

<figure>
  <img src="/assets/images/GS_dashboard_explore_reports.png" width="800"/>
  <figcaption>Editing Reports On A Dashboard</figcaption>
</figure>

## Dimensions
Dimensions is a primary concept when exploring your data. Dimensions are attributes and characteristics of your data. For example, in the domain of web analytics, dimensions might include properties of your website users: gender, age, location, etc. Dimensions can be used to partition your data into slices, and to focus on a specific slice using filters. In Yavin, dimensions live in the dimension panel in the report. They can be searched by, filtered by and added to the report for insights and reporting.

<figure>
  <img src="/assets/images/GS_Dimensions.gif"/>
  <figcaption>Yavin Dimensions Selector</figcaption>
</figure>

[How to define dimensions in your model language?][adding-columns]

Measures
-------------------------------
Measures, also known as ***metrics***, provide a numeric value associated with one or more dimensions. Yavin has the ability to represent any aggregate computation supported by your database as a measure.  Common examples for measures include counting, summing, averaging, or taking ratios of columns in your data.  Measures live in the Metrics Panel in the report. They can be searched for, filtered by, and added to the report.

<figure>
  <img src="/assets/images/GS_metrics.gif"/>
  <figcaption>Yavin Measures Selector</figcaption>
</figure>

[How to define measures in your model language?][adding-columns]

[adding-columns]: https://elide.io/pages/guide/v5/04-analytics.html#columns
