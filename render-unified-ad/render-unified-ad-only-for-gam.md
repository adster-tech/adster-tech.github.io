---
description: Below are the steps to load and render a unified ad on your app
---

# 🎨 Render Unified Ad (Only for GAM)

1. Create your `AdRequestConfiguration` as per the below format

{% code overflow="wrap" %}
```java
val configuration = AdRequestConfiguration(context, "Your_placement_name")
```
{% endcode %}

2. Call `loadAd()` method as per the below format

{% code overflow="wrap" %}
```java
AdSter.INSTANCE.loadAd(configuration, new AdsEventListener() {
  @Override
    public void onNativeAdLoaded(@NonNull MediationNativeAd ad) {
      super.onNativeAdLoaded(ad);
    }

  @Override
    public void onBannerAdLoaded(@NonNull MediationBannerAd ad) {
      super.onBannerAdLoaded(ad);
    }

  @Override
    public void onFailure(@NonNull AdError adError) {
      // Handle Failure here
    }
});
```
{% endcode %}

{% hint style="info" %}
`onNativeAdLoaded()` - [Click here](../how-to-render-an-ad/native-ad.md#kotlin) for Rendering implementation\
`onBannerAdLoaded()` - [Click here](../how-to-render-an-ad/banner-ad.md) for Rendering implementation
{% endhint %}

## Manifest Changes Required for SDK

Please add these changes to the manifest of your application.

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
