---
layout: guide
group: guide
title: Product Overview
---

Yavin is a framework for rapidly **building custom data applications** that offers both a UI and an API. In addition, Yavin can be deployed as a **standalone Business Intelligence tool** allowing users to explore and drill into data through an intuitive interface.  Yavin provides a set of modular **user experience blocks** that can be customized and assembled into a complete data application.  The most common blocks are **reports** and **dashboards**.  Reports allow users to craft, execute, and visualize adhoc queries.  Reports can be assembled into dashboards that collate related visualizations together.  Yavin includes a powerful **semantic layer** that lets you model and deploy the tables, measures, and dimensions users will see and select throughout the user experience.

<video controls> <source src="/assets/images/Yavin_in_action.mov"></video>

Yavin is consistent of three separate repository that can all be accessed from [https://github.com/yavin-dev/](https://github.com/yavin-dev/):
1. ***app*** : Containing only the simplified app used as a standalone BI tool or to build your custom data applications.
2. ***framework*** : The entire UI framework. Including dependencies. This should only be used if you would like to contribute to Yavin as a framework.
3. ***docs*** : This repository serves as documentation repo for Yavin

***Disclaimer*** : For the sample demos that come with Yavin, we are using the [Netflix Movie and TV Shows](https://www.kaggle.com/shivamb/netflix-shows) dataset that is sourced from [Kaggle](https://www.kaggle.com) (Timestamped 11/2020). The use of this dataset is only in demonstrating the ease of onboarding any dataset to Yavin. It has no correlation with the Yavin project.

## Customizable Building Blocks
In the software industry, when discovering patterns, we often build abstractions and libraries to provide reusable software. The D3.js charting library, Spring Security, and the Flask web framework are all great examples. While these provide a significant productivity gain, especially when compared to writing everything from scratch, it still is costly to build applications. When building applications, it takes time to design a system, wire together libraries, test your logic, build a web service, develop a great user interface and battle test your system.  Yavin's building blocks are conceptually larger than a library - enabling larger patterns of software reuse. There is a tradeoff here, though: these building blocks are not as flexible as writing code from scratch. So you gain in functionality but you lose some ability to customize.

## Yavin’s Main Components

Yavin is composed of three open source modules.

### Denali: Themeable Design System

**Yavin uses Denali's theme-able design system**. Denali was developed as a way to quickly create unified product families with intuitive user experiences. Denali components are built to be theme-able by nature, which means we aren’t tied to their components visual design.

For more information on Denali, visit [denali.design](https://denali.design).

### Elide: A Model Driven API & Semantic Layer

**Yavin uses Elide as its web service and semantic layer**. Elide is a Java library that lets you build model driven GraphQL or JSON-API web services with minimal effort. Elide supports two variants of APIs:

1. A CRUD (Create, Read, Update, Delete) API for reading and manipulating models.
1. An analytic API for aggregating measures over zero or more model dimensions.

For more information on Elide, visit [elide.io](https://elide.io).

### Yavin: User Interface Building Blocks

**Yavin contains the User Interface layer**.  Yavin uses Ember - a JavaScript framework for building modern web applications. It includes everything you need to build rich UIs that work on any device.

For more information on Ember.js, visit [emberjs.org](https://emberjs.com/).
