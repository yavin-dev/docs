---
layout: guide
group: guide
title: Quick Start Guide
date: 2021-03-16
---

## Prerequisites

Before getting started with Yavin, make sure to have:

### <img src="/assets/images/mac_icon.png" alt="mac logo" style="height: 40px; margin-bottom: -8px"> For macOS

1. **Java 8 or greater** - You can check by running ```java -version```.
    > Free prebuilt OpenJDK binaries are available on **[https://adoptopenjdk.net](https://adoptopenjdk.net)**.
    {:.info}

2. **Git** - You can check by running ```git --version```

### <img src="/assets/images/windows_icon.png" alt="windows logo" style="height: 40px; margin-bottom: -10px"> For Windows

1. **Windows Subsystem for Linux** - You can follow [this guide](https://docs.microsoft.com/en-us/windows/wsl/install-win10) to enable it
2. An [**Ubuntu distribution**](https://www.microsoft.com/store/apps/9N9TNGVNDL3Q) 
3. **Java 8 or greater** - You can install it by running
    > ```shell
    > sudo apt-get update
    > sudo apt-get install default-jdk
    > ```
    >
    > Make sure it is working by running ```java -version```
    {:.info}

4. **Git** - You can check by running ```git --version``` but it should come installed

## Boot Example Yavin App Locally

Once you are all set up, run the following steps (On ***Terminal*** for macOS, and on ***Bash*** for Windows) to boot the example Yavin app:

> There is currently a bug that requires your locale to be set otherwise your app may crash.
>
> If you see an error like `Error parsing "September 9, 2019"`, run `export LANG=en_US.UTF-8`
{:.warning}

### 1.1 (Option 1) Run Jar Locally

To kick of your custom data application building, you will only need the app repo.

```shell
git clone https://github.com/yavin-dev/app.git
./gradlew bootRun                           
```

### 1.2 (Option 2) Launch Demo App in Docker Container

If local port is different then change the argument in below command. Format is ```-p <host port>:<container port>```

```shell
docker run -p 8080:8080 docker.io/verizonmedia/yavin_demo:latest
```

(To stop the server at any time, type Ctrl-C in your terminal.)

### 2. Open The App In Your Browser

Congratulations! You can now open **[http://localhost:8080](http://localhost:8080)**. This will launch the **Yavin** application into your browser with the built in data set for [Netflix and TV shows](https://www.kaggle.com/shivamb/netflix-shows) that is sourced from [Kaggle](https://www.kaggle.com/) data.


### Steps In Action

<video controls class="m-t-20">
  <source src="/assets/images/QS_installation_and_run.mp4" type="video/mp4">
</video>

The video above is a recording of the steps required to boot the Yavin example app.

## Helpful Links

For a more extended list of commands that can be done once you clone the repo, please check: [https://github.com/yavin-dev/app#getting-started](https://github.com/yavin-dev/app#getting-started)

| Info                     |  Link  |
|---------------------------------|--------|
| **Git Setup**  | [https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup) |
| **AdoptOpenJDK**  | [https://adoptopenjdk.net/index.html](https://adoptopenjdk.net/index.html) |
| **Yavin App Repo**  |  [https://github.com/yavin-dev/app.git](https://github.com/yavin-dev/app.git) |
| **Demo Data** | [https://www.kaggle.com/shivamb/netflix-shows](https://www.kaggle.com/shivamb/netflix-shows) |
{:.table}
