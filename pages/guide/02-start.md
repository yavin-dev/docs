---
layout: guide
group: guide
title: Quick Start Guide
---


## Prerequisites

Before getting started with Yavin, make sure your system has **Java 8 or greater**. You can find free prebuilt OpenJDK binaries at **[https://adoptopenjdk.net](https://adoptopenjdk.net)**.

## Boot Example Yavin App Locally

Once your machine has all met the prerequisites, run the following steps to boot the example Yavin app:

### 1. Clone the project

```shell
git clone https://github.com/yahoo/yavin.git
```

### 2.1 (Option 1): Run Jar Locally

```shell
cd yavin/packages/webserivce                 
./gradlew bootRun                           
```
### 2.2 (Option 2): Launch Demo App in Docker Container

```shell
docker run docker.io/verizonmedia/yavin:demo_local
```

(To stop the server at any time, type Ctrl-C in your terminal.)

### 3. Open The App In Your Browser

Congratulations! You can now open **[http://localhost:8080](http://localhost:8080)**. This will launch the **Yavin** application into your browser with the built in data set for [Netflix and TV shows](https://www.kaggle.com/shivamb/netflix-shows) that is sourced from [Kaggle](https://www.kaggle.com/) data.


### Steps In Action

<video controls class="m-t-20">
  <source src="/assets/images/QS_installation_and_run.mp4" type="video/mp4">
</video>

The video above is a recording of the steps required to boot the Yavin example app.

## Helpful Links

| Info                     |  Link  |
|---------------------------------|--------|
| **Git Setup**  | [https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup) |
| **AdoptOpenJDK**  | [https://adoptopenjdk.net/index.html](https://adoptopenjdk.net/index.html) |
| **Yavin Repo**  |  [https://github.com/yahoo/yavin.git](https://github.com/yahoo/yavin.git) |
| **Demo Data** | [https://www.kaggle.com/shivamb/netflix-shows](https://www.kaggle.com/shivamb/netflix-shows) |
{:.table}
