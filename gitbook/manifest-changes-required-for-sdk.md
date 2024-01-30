---
description: Please add these changes to the manifest of your application
---

# Manifest Changes Required for SDK

{% code overflow="wrap" %}
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="com.google.android.gms.permission.AD_ID"/>
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```
{% endcode %}

***

{% hint style="warning" %}
If you don\`t have an admob account and want to test the initialization of the SDK, please also add these to the manifest so that the SDK initialization can be completed.
{% endhint %}

{% code overflow="wrap" %}
```xml
<meta-data android:name="com.google.android.gms.ads.APPLICATION_ID" android:value="ca-app-pub-7640426597645136~3443205346" />
```
{% endcode %}
