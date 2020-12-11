---
layout: guide
group: guide
title: Getting Started with the UI
---

* TOC
{:toc}


Directory / “My Data” / landing Page
----------------------------------------------
The default landing page of Yavin is the start of your data exploration. The Directory/“My Data” view carries all the active reports (individual data visualizations) / Dashboards (a group of related reports) that you have previously created as well as any reports and dashboards that have been shared with you.

Within the Directory view you can:
- Create new Reports and/or Dashboards
- Filter based on your “Favorites” Reports/Dashboards
- Search for specific Reports/Dashboards
- Filter by Reports/Dashboards
- Perform actions on a report (Clone, Export, Share, Schedule, Delete)
- Perform actions on a dashboard (Clone, Export, Share,Delete)

<figure style="font-size:0.6vw; color:DodgerBlue;"><img style="border:2px solid black;" src="/assets/images/GS_my_data_list.gif" width="800"/><figcaption>Gif animation - Browsing the directory view </figcaption> </figure>

#### Directory View Operations
What can you do in the directory view of Yavin? Let’s explore these options one at a time.

##### Perform actions on a report:
<img src="/assets/images/GS_report_options.png" width="400"/>

|      Operation                      |  Availability                       |
|---------------------------------|---------------------------------------|
| <img src="/assets/images/GS_my_data_new_report.png" width="150"/> | Now         |
| Clone ![Clone](/assets/images/GS_clone.png) | Now |
| Export ![Export](/assets/images/GS_download.png) | Q1  2021 |
| Share ![Share](/assets/images/GS_share.png)  | Now |
| Delete ![Delete](/assets/images/GS_delete_icon.png) | Now         |
{:.table}

##### Perform actions on a Dashboard:
<img src="/assets/images/GS_dashboard_options.png" width="400"/>

|      Operation                      |  Availability                       |
|---------------------------------|---------------------------------------|
| <img src="/assets/images/GS_my_data_new_dashboard.png" width="150"/>  | Now         |
| Clone ![](/assets/images/GS_clone.png) | Now          |
| Share ![](/assets/images/GS_share.png)  | Now        |
| Delete ![](/assets/images/GS_delete_icon.png) | Now         |
{:.table}

Reports
-------------------------------
A report is a user defined query coupled with a visual representation (table, graph, etc) of the returned query result. With a report, you can freely explore the various dimensions and measures of your data. Shown below is a line chart visualization from a report showing the “Netflix TV shows release dates”, filtering only for TV shows, and release date equal to 2014. With “Release Date” as dimension and “Total Seasons” and “Count” as measures.

<figure style="font-size:0.6vw; color:DodgerBlue;"><img style="border:2px solid black;" src="/assets/images/GS_Yavin_report_in_action.gif" width="800"/><figcaption>Gif animation - Yavin report in action </figcaption> </figure>

#### The high level operations on a report include:

![](/assets/images/GS_report_action_long_list.png)

From within the report you have multiple options. Each option is shown with its associated screen icon. You can do any of the following:
You can rename, add to favorite, add to dashboard, copy API query, clone, export, share and delete.


|      Operation                  |  Availability                       |
|---------------------------------|-------------------------------------|
| Rename   ![](/assets/images/GS_edit.png)  | Now         |
| Add too Favorite     ![](/assets/images/GS_star.png)       |     Now          |
| ![](/assets/images/GS_add_to_dashboard_withText.png) | Now          |
| ![](/assets/images/GS_copy_api_query_withText.png)  | Now        |
| ![](/assets/images/GS_clone_with_text.png) | Now         |
| ![](/assets/images/GS_export_with_text.png)     |   Q1 2021   |
| ![](/assets/images/GS_share_withText.png)     |  Now    |
| ![](/assets/images/GS_delete.png)     |  Now    |
{:.table}

All operations are associated with a tool tips guide:
<figure style="font-size:0.6vw; color:DodgerBlue;"><img src="/assets/images/GS_report_action_anima.gif" width="800"/><figcaption>Gif animation - Tooltips will guide you to the actions in a report </figcaption> </figure>

At any time in a report, you can perform one of the following operations : Run, Save, Save As, Revert
![](/assets/images/GS_report_action.png)

### Exploring Reports
Reports are designed to be explored intuitively, easily and quickly.


1.  Create a new report from Yavin’s directory view
<img src="/assets/images/GS_my_data_new_report.png" width="100"/>
1.  Select a table
![](/assets/images/GS_table_selector.png)
1.  Select a dimension
<img src="/assets/images/GS_dimension_selector.png" width"200"/>
1.  Select a measure
<img src="/assets/images/GS_metric_selector.png" width"200"/>
1.  Update your filters
![](/assets/images/GS_report_filter_sample.png)
1.  Select run report button
![](/assets/images/GS_run_saveReport.png)

Here is a brief, animated demo showing how to explore and run a Yavin report :
<figure style="font-size:0.6vw; color:DodgerBlue;"> <img style="border:2px solid black;" src="/assets/images/GS_managing_reports.gif" width="800"/><figcaption>Gif animation - Exploring reports “in action” </figcaption> </figure>

Dashboards
----------------------------------
Yavin lets you take multiple reports and organize them into a dashboard even if the reports have different visualizations. Dashboards allow you to position and size the individual reports as you desire. They are useful when your user may need to compare various reports or take multiple views of data into account.

<figure style="font-size:0.6vw; color:DodgerBlue;"><img style="border:2px solid black;" src="/assets/images/GS_dashboard_sample.png" width="800" /><figcaption>Figure - A Typical Yavin Dashboard with a collection of widgets/reports </figcaption> </figure>

From within a Dashboard, you can do all of the following. The on-screen icon is shown beside the command:

![](/assets/images/GS_dashboard_options_long_list.png)

|      Operation                      |  Availability                       |
|---------------------------------|---------------------------------------|
| Rename ![](/assets/images/GS_edit.png)   | Now         |
| Add too Favorite ![](/assets/images/GS_star.png) |     Now          |
| ![](/assets/images/GS_clone_with_text.png) | Now         |
| ![](/assets/images/GS_share_withText.png)     |  Now    |
| ![](/assets/images/GS_delete.png)     |  Now    |
| <img src="/assets/images/GS_add_widget.png" width="100"/>   |  Now    |
| ![](/assets/images/GS_settings_add_filter.png)     |  Now    |
{:.table}

At any time in a dashboard, you can perform one of the following operations : Save Changes, Revert Changes
![](/assets/images/GS_dashboard_action.png)

### Exploring and Managing Dashboards:
Dashboards are designed for intuitive data exploration.

<figure style="font-size:0.6vw; color:DodgerBlue;"><img style="border:2px solid black;" src="/assets/images/GS_managing_dashboard.gif" width="800"/><figcaption>Gif animation - Exploring dashboards “in action” </figcaption> </figure>

Dashboards are built by adding reports to them one at a time. There are two ways of adding a report to a dashboard.
- Through the Dashboard view.
- Through the report view.

#### Adding Reports to a Dashboard from the Dashboard view
From the dashboard itself, use the “+ Add Widget” button :

1.  Select <img src="/assets/images/GS_add_widget.png" width="150"/> to add an already existing report to the Dashboard
1.  Select the report like this: ![](/assets/images/GS_add_widget_dialog.png)
1.  You can choose between creating a new report or using an existing one : <img src="/assets/images/GS_add_widget2.png" width="350"/> <img src="/assets/images/GS_add_search_widget.png" width="350"/>
1.  The Report will be added to the dashboard as a widget: ![](/assets/images/GS_table_row.png)
1.  The Report/Widget can be resized, edited and deleted: ![](/assets/images/GS_table_sample.png)

#### Adding Reports to a Dashboard from the Report view
1. A report can be added to the dashboard by selecting a previously saved report through the “Add to Dashboard” option as illustrated: <img src="/assets/images/GS_dashboard_tool_tip.png" width="300"/>
1. You can choose to create a new Dashboard, or to add the report to an existing dashboard: ![](/assets/images/GS_add_to_dashboard.png)   ![](/assets/images/GS_add_to_dashboard_select_widget.png)

#### Modifying / Editing Dashboards:
The reports/widgets in a dashboard can be organized, resized, explored, filtered and edited to align with how you want the Dashboard to look. Reports in a Dashboard can be edited by clicking on the pencil icon (![](/assets/images/GS_edit.png" width="50"/>) in the header of the widget/report. This will activate the edit mode for that report. Reports in a dashboard can also be resized, re-arranged and deleted.

<figure style="font-size:0.6vw; color:DodgerBlue;"><img style="border:2px solid black;" src="/assets/images/GS_dashboard_explore_reports.png" width="800"/><figcaption>Figure - Editing reports on a dashboard</figcaption> </figure>

Dimensions
----------------------------------
Dimensions are the primary concept when exploring your data. Dimensions are attributes and characteristics of your data. For example: In the domain of web analytics, dimensions might include properties of your website users: gender, age, location, etc. Dimensions can be used to partition your data into slices, and to focus on a specific slice using filters. In Yavin, Dimensions live in the dimension panel in the report. They can be searched by, filtered by and added to the report for insights and reporting.

<figure style="font-size:0.6vw; color:DodgerBlue;"><img style="border:2px solid black;" src="/assets/images/GS_Dimensions.gif" /><figcaption>Gif animation - Yavin dimensions explorer / selector</figcaption> </figure>

[How to define dimensions in your model language?][adding-columns]

Measures
-------------------------------
Measures provide a numeric value associated with one or more dimensions. Yavin has the ability to represent any aggregate computation supported by your database as a measure.  Common examples for measures include counting, summing, averaging, or taking ratios of columns in your data.  Measures live in the Metrics Panel in the report. They can be searched for, filtered by, and added to the report.

<figure style="font-size:0.6vw; color:DodgerBlue;"><img style="border:2px solid black;" src="/assets/images/GS_metrics.gif" /><figcaption>Gif animation - Yavin measures explorer / selector</figcaption> </figure>

[How to define measures in your model language?][adding-columns]

[adding-columns]: https://elide.io/pages/guide/v5/04-analytics.html#columns
