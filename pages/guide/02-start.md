---
layout: guide
group: guide
title: Quick Start Guide
---

* TOC
{:toc}

## Helpful Links

| Info                     |  Link  |
|---------------------------------|--------|
| Getting Started - First-Time Git Setup  | [https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup) |
| Prerequisite - JDK 8 or higher  |  [https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html) |
| Yavin Git Repo  |  [https://github.com/yahoo/navi.git](https://github.com/yahoo/navi.git) |
| Netflix Movies and TV Shows" data set used for the demo | [https://www.kaggle.com/shivamb/netflix-shows](https://www.kaggle.com/shivamb/netflix-shows) |
{:.table}

## Setup Steps

| Step                            | Description |
|---------------------------------|-------------|
| git clone https://github.com/yahoo/navi.git | Clone the yavin repository |
| cd navi/packages/webserivce                 | Change directories to build the application |
| ./gradlew bootRun                           | build and run the application |
{:.table}

** Ctrl-C to Exit **


<figure style="font-size:0.6vw; color:DodgerBlue;">
    <video controls> <source src="/assets/images/QS_installation_and_run.mp4" type="video/mp4"></video>
    <figcaption>A quick video that shows Yavin quick setup steps.</figcaption>
</figure>


***Congratulations!  You can now open [http://localhost:8080](http://localhost:8080).*** This will launch the **Yavin** application into your browser with the built in data set for [Netflix and TV shows](https://www.kaggle.com/shivamb/netflix-shows) that is sourced from [Kaggle](https://www.kaggle.com/) data.
