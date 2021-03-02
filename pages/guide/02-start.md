---
layout: guide
group: guide
title: Quick Start Guide
---

## Prerequisites

Before getting started with Yavin, make sure :

### ![](/assets/images/mac_icon.png) For MAC

1. Check if your system has **Java 8 or greater**, you can check so with . You can find free prebuilt OpenJDK binaries at **[https://adoptopenjdk.net](https://adoptopenjdk.net)**.

Or on the terminal, install it using:
```shell
    sudo apt-get update
    sudo apt-get install default-jdk
```
Check again: ```java -version```

2. See if Git is installed by executing: ```git --version```
If not then install it using:

```shell
    sudo apt-get update
    sudo apt-get install git
```
Check again: ```git --version```


### ![](/assets/images/windows_icon.png) For Window

1. Install Bash on Windows 10: [https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/](https://www.howtogeek.com/249966/how-to-install-and-use-the-linux-bash-shell-on-windows-10/)
2. Next, launch the [Ubuntu distribution](https://en.wikipedia.org/wiki/Ubuntu):
3. Via the Bash environment, see if java is installed by executing: ```java -version```. If not then install it using: (***Do not try to use java installation for windows***)
```shell
    sudo apt-get update
    sudo apt-get install default-jdk
```
Check again: ```java -version```

4. Via the Bash environment, see if Git is installed by executing: ```git --version```
If not then install it using:

```shell
    sudo apt-get update
    sudo apt-get install git
```
Check again: ```git --version```

## Boot Example Yavin App Locally

Once your machine has all met the prerequisites, run the following steps (On ***Terminal*** for MAC, and on ***Bash*** for Windows)to boot the example Yavin app:

### 1.1 (Option 1) Run Jar Locally

Yavin is consistent of 3 separate repository that can all be accessed from [https://github.com/yavin-dev/](https://github.com/yavin-dev/):
1. ***app*** : Containing only the simplified app used as a standalone BI tool or to build your custom data applications.
2. ***framework*** : The entire UI framework. Including dependencies. This should only be used if you would like to contribute to Yavin as a framework.
3. ***docs*** : This repository serves as documentation repo for Yavin

To kick of your custom data application building, you will only need the app repo.

```shell
git clone https://github.com/yavin-dev/app.git
```

### 2.1 (Option 1): Run Jar Locally

```shell
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
