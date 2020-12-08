---
layout: guide
group: guide
title: Product Overview
---

* TOC
{:toc}

## Yavin overview
<img src="assets/images/Yavin_logo.png" width="200"/>

Yavin is a framework for rapidly **building custom data applications** that offers both a UI and an API. In addition, Yavin can be deployed as a **standalone Business Intelligence tool** allowing users to explore and drill into data through an intuitive interface.  Yavin provides a set of modular **user experience blocks** that can be customized and assembled into a complete data application.  The most common blocks are **reports** and **dashboards**.  Reports allow users to craft, execute, and visualize adhoc queries.  Reports can be assembled into dashboards that collate related visualizations together.  Yavin includes a powerful **semantic layer** that let's you model and deploy the tables, measures, and dimensions users will see and select throughout the user experience.

***Disclaimer*** : For the sample demos that come with Yavin, we are using the [Netflix Movie and TV Shows](https://www.kaggle.com/shivamb/netflix-shows) data set that is sourced from [Kaggle](https://www.kaggle.com) (Timestamped 11/2020). The use of this data-set is only in demonstrating the ease of onboarding any dataset to Yavin. It has no correlation with the Yavin project.

## Components

Yavin is a composed of three open source modules.  They are:
- [Denali](https://denali.design/) - A themeable user interface design language.
- [Elide](https://elide.io) - A model driven API framework and Yavin's semantic layer.
- [Yavin](https://github.io/yahoo/navi) - The user interface building blocks.

Here is a short video of Yavin “in action” :

<figure style="font-size:0.6vw; color:DodgerBlue;"><img style="border:2px solid black;" src="assets/images/Get_to_know_yavin.gif" width="800" /><figcaption>Gif animation - Yavin simplicity “in action”</figcaption></figure>

## Building with Legos ® & Duplos ®
In the software industry, when discovering patterns, we often build abstractions and libraries to provide reusable software. The D3.JS charting library, Spring Security, and the Flask web framework are all great examples. We often use the metaphor building with Legos ® to illustrate the process of building software with many libraries and frameworks. While this provides a significant productivity gain, especially when compared to writing everything from scratch, it still is costly to build applications. When building applications, it takes time to design a system, wire together libraries, test your logic, build a web service, develop a great user interface and battle test your system. A Duplo is a reusable block of functionality that is conceptually larger than a library that enables larger patterns of software reuse. There is a tradeoff here though. Duplos ® are not as flexible as writing code from scratch. So you gain in functionality but you lose some ability to customize. With Yavin, we aim to package fully featured and reusable block of functionality called Duplos ®, or large Legos®, that can be installed in your application with a few commands. The following diagram illustrates the Duplos® available in Yavin today:

<figure style="font-size:0.6vw; color:DodgerBlue;"><img src="assets/images/Duplos_img.png" width="800" border=5px/><figcaption>Figure - Yavin Duplos</figcaption></figure>

## An Overview of Yavin’s Main Components

### Denali Overview
<img src="assets/images/Denali_logo.png" width="200"/>

**Yavin uses Denali's theme-able design system**. Denali was developed as a way to quickly create unified product families with intuitive user experiences. Denali components are built to be theme-able by nature, which means we aren’t tied to their components visual design. For more information on denali, visit <a href="http://denali.design" >denali.design</a>.

### Elide Overview
<img src="assets/images/Elide_logo.png" width="200"/>

**Yavin uses Elide as its web service and data model building language**. Elide is a Java library that lets you setup model driven GraphQL or JSON-API web services with minimal effort. Elide supports two variants of APIs:
1.  A CRUD (Create, Read, Update, Delete) API for reading and manipulating models.
1.  An analytic API for aggregating measures over zero or more model dimensions.

For more information on Elide, visit <a href="http://elide.io">elide.io</a>

### Navi Overview
<img src="assets/images/Navi_logo.png" width="200"/>

**Navi represents the User Interface layer of Yavin**. Navi is an open source analytics reporting UI. Navi uses Ember, which is a JavaScript framework for building modern web applications. It includes everything you need to build rich UIs that work on any device. (<a href="https://guides.emberjs.com">Ember Guide</a>)
