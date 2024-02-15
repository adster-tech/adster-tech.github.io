---
description: Below are the steps to load and render a unified ad on your app
---

# 🎨 Render Unified Ad (Only for GAM)

1. Create your `AdRequestConfiguration` as per the below format

{% code overflow="wrap" %}
```java
val configuration = AdRequestConfiguration.Companion.builder(context, "Your_placement_name");
```
{% endcode %}

2. Call `loadAd()` method as per the below format

{% tabs %}
{% tab title="Java" %}
```java
AdSterAdLoader.Companion.builder().withAdsListener(new MediationAdListener() {
    @Override
    public void onBannerAdLoaded(@NonNull MediationBannerAd ad) {
        super.onBannerAdLoaded(ad);
        //Show banner ad here
    }

    @Override
    public void onNativeAdLoaded(@NonNull MediationNativeAd ad) {
        super.onNativeAdLoaded(ad);
        //Show native ad here
    }

    @Override
    public void onNativeCustomFormatAdLoaded(@NonNull MediationNativeCustomFormatAd ad) {
        super.onNativeCustomFormatAdLoaded(ad);
        //Show native custom format ad here
    }

    @Override
    public void onFailure(@NonNull AdError adError) {
        //Handle failure callback here
    }
}).withAdsEventsListener(new AdEventsListener() {
    @Override
    public void onAdClicked() {
        //Handle ad click here
    }

    @Override
    public void onAdImpression() {
        //Handle ad impression here
    }
}).build().loadAd(configuration.build());
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
AdSterAdLoader.builder().withAdsListener(object : MediationAdListener() {
    override fun onBannerAdLoaded(ad: MediationBannerAd) {
        super.onBannerAdLoaded(ad)
        //Show banner ad here
    }

    override fun onNativeAdLoaded(ad: MediationNativeAd) {
        super.onNativeAdLoaded(ad)
        //Show native ad here
    }

    override fun onNativeCustomFormatAdLoaded(ad: MediationNativeCustomFormatAd) {
        super.onNativeCustomFormatAdLoaded(ad)
        //Show native custom format ad here
    }

    override fun onFailure(adError: AdError) {
        //Handle failure callback here
    }
}).withAdsEventsListener(object : AdEventsListener() {
    override fun onAdClicked() {
        //Handle ad click here
    }

    override fun onAdImpression() {
        //Handle ad impression here
    }
}).build().loadAd(configuration.build())
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
`onNativeAdLoaded()` - [Click here](../how-to-render-an-ad/native-ad.md#kotlin) for Rendering implementation\
`onBannerAdLoaded()` - [Click here](../how-to-render-an-ad/banner-ad.md) for Rendering implementation\
`onNativeCustomFormatAdLoaded()` - [Click here](../how-to-render-an-ad/native-ad-1.md) for Rendering implementation
{% endhint %}
