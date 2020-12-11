---
layout: guide
group: guide
title: Product Overview
---
* TOC
{:toc}

## Yavin overview
![Yavin Logo](/assets/images/Yavin_logo.png){:class="img-responsive"}

Yavin is a framework for rapidly **building custom data applications** that offers both a UI and an API. In addition, Yavin can be deployed as a **standalone Business Intelligence tool** allowing users to explore and drill into data through an intuitive interface.  Yavin provides a set of modular **user experience blocks** that can be customized and assembled into a complete data application.  The most common blocks are **reports** and **dashboards**.  Reports allow users to craft, execute, and visualize adhoc queries.  Reports can be assembled into dashboards that collate related visualizations together.  Yavin includes a powerful **semantic layer** that let's you model and deploy the tables, measures, and dimensions users will see and select throughout the user experience.

***Disclaimer*** : For the sample demos that come with Yavin, we are using the [Netflix Movie and TV Shows](https://www.kaggle.com/shivamb/netflix-shows) data set that is sourced from [Kaggle](https://www.kaggle.com) (Timestamped 11/2020). The use of this data-set is only in demonstrating the ease of onboarding any dataset to Yavin. It has no correlation with the Yavin project.

## Components

Yavin is a composed of three open source modules.  They are:
- [Denali](https://denali.design/) - A themeable user interface design language.
- [Elide](https://elide.io) - A model driven API framework and Yavin's semantic layer.
- [Yavin](https://github.io/yahoo/navi) - The user interface building blocks.

Here is a short video of Yavin “in action” :

<figure>
    <video controls> <source src="/assets/images/Yavin_in_action.mov"></video>
    <figcaption>Yavin simplicity “in action”.</figcaption>
</figure>

## Customizable Building Blocks
In the software industry, when discovering patterns, we often build abstractions and libraries to provide reusable software. The D3.JS charting library, Spring Security, and the Flask web framework are all great examples. While these provide a significant productivity gain, especially when compared to writing everything from scratch, it still is costly to build applications. When building applications, it takes time to design a system, wire together libraries, test your logic, build a web service, develop a great user interface and battle test your system.  Yavin build blocks are conceptually larger than a library - enabling larger patterns of software reuse. There is a tradeoff here though.  These building blocks are not as flexible as writing code from scratch. So you gain in functionality but you lose some ability to customize. The following diagram illustrates the building blocks available in Yavin today:

<figure><img src="/assets/images/Duplos_img.png"/>
    <figcaption>Figure - Yavin Building Blocks</figcaption>
</figure>

## An Overview of Yavin’s Main Components

### Denali Overview
![Denali Logo](/assets/images/Denali_logo.png){:class="img-responsive"}

**Yavin uses Denali's theme-able design system**. Denali was developed as a way to quickly create unified product families with intuitive user experiences. Denali components are built to be theme-able by nature, which means we aren’t tied to their components visual design. For more information on denali, visit [denali.design](https://denali.design).

### Elide Overview
![Elide Logo](/assets/images/Elide_logo.png){:class="img-responsive"}

**Yavin uses Elide as its web service and semantic layer**. Elide is a Java library that lets you setup model driven GraphQL or JSON-API web services with minimal effort. Elide supports two variants of APIs:
1.  A CRUD (Create, Read, Update, Delete) API for reading and manipulating models.
1.  An analytic API for aggregating measures over zero or more model dimensions.

For more information on Elide, visit [elide.io](https://elide.io).

### Navi Overview
![Navi logo](/assets/images/Navi_logo.png){:class="img-responsive"}

**Yavin contains the User Interface layer**.  Yavin uses Ember - a JavaScript framework for building modern web applications. It includes everything you need to build rich UIs that work on any device. [Ember Guide](https://guides.emberjs.com).
