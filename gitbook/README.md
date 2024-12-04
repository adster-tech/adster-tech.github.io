---
description: >-
  This guide provides a comprehensive step-by-step process for integrating the
  AdSter SDK into your Android application. Ensure you follow each section
  carefully for successful implementation
---

# 📱 SDK Implementation Guide

{% hint style="info" %}
**App Prerequisite**

* minSdkVersion of 21 or higher
* compileSdkVersion of 33 or higher
{% endhint %}

## Configuration Steps



**Setting Up Repository in Project**

* Open your Android Studio project and navigate to `settings.gradle` file
* Add the following Maven repository configuration inside the dependencyResolutionManagement block

```java
gradle

repositories {
  ...
  maven {
    url = uri("https://maven.pkg.github.com/adster-tech/orchestration-sdk")
    credentials {
      username = GITHUB_USERNAME
      password = GITHUB_TOKEN
    }
  }
}
```

{% hint style="warning" %}
Replace GITHUB\_USERNAME and GITHUB\_TOKEN with your GitHub username and personal access token.
{% endhint %}

***

**Adding Dependency**

* Open the `build.gradle` (Module: app) file.
* Find the dependencies block and add the following SDK dependency.

```java
gradle

implementation 'com.adster:orchestrationsdk:1.1.08'
```

***

**Authentication**

* It's crucial not to hardcode GitHub credentials. Store credentials in `gradle.properties` or use environment variables.
*   In `gradle.properties`, add

    ```
    properties

    GITHUB_USERNAME=username
    GITHUB_TOKEN=token
    ```
*   In `settings.gradle`,  reference these properties:

    ```
    gradle

    username = findProperty("GITHUB_USERNAME") ?: System.getenv("GITHUB_USERNAME")
    password = findProperty("GITHUB_TOKEN") ?: System.getenv("GITHUB_TOKEN")
    ```

{% hint style="success" %}
This approach enhances security by keeping credentials out of source control.
{% endhint %}
