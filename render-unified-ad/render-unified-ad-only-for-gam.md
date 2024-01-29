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

```java
AdSter.INSTANCE.loadAd(configuration, new AdsEventListener() {
  @Override
    public void onNativeAdLoaded(@NonNull MediationNativeAd ad) {
      super.onNativeAdLoaded(ad);
    }
    
  @Override
    public void onNativeCustomFormatAdLoaded(@NonNull MediationNativeCustomFormatAd ad) {
      super.onNativeCustomFormatAdLoaded(ad);
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

{% hint style="info" %}
`onNativeAdLoaded()` - [Click here](../how-to-render-an-ad/native-ad.md#kotlin) for Rendering implementation\
`onBannerAdLoaded()` - [Click here](../how-to-render-an-ad/banner-ad.md) for Rendering implementation\
`onNativeCustomFormatAdLoaded()` - [Click here](../how-to-render-an-ad/native-ad-1.md) for Rendering implementation
{% endhint %}
