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

## **Manifest Changes Required for SDK**

Please add these changes to the manifest of your application

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="com.google.android.gms.permission.AD_ID"/>
```

{% hint style="warning" %}
If you don't have an admob account and want to test the initialization of the SDK, please also add these to the manifest so that the SDK initialization can be completed.
{% endhint %}

```xml
<meta-data android:name="com.google.android.gms.ads.APPLICATION_ID"
android:value="ca-app-pub-3940256099942544~3347511713" />
```

## Configuration Steps

**Adding Dependency**

* Open the `build.gradle` (Module: app) file.
* Find the dependencies block and add the following SDK dependency.
* Add these proguard rules / lines in the final release build\
  -keep class com.adster.\*\* { \*; }

{% code fullWidth="true" %}
```
implementation 'com.adstertech:orchestrationsdk-lite:2.2.1'
```
{% endcode %}
