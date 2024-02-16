---
description: >-
  Below are the steps to pass PPID with ad request for GAM (Supported by all ad
  formats)
---

# 🎨 How to pass publisher provided identifiers in ad request (PPID) (Only for GAM)

1. Create your `AdRequestConfiguration` as per the below format

{% code overflow="wrap" %}
```java
val configuration = AdRequestConfiguration.Companion.builder(context, "Your_placement_name");
```
{% endcode %}

2. Adding PPID to AdRequest

{% code overflow="wrap" %}
```java
configuration.publisherProvidedId("YOUR_PPID");
```
{% endcode %}

{% hint style="info" %}
#### PPID can be passed for all ad type ad requests.

Here is an example of implementation with banner ad.
{% endhint %}

3. Call `loadAd()` method as per below format

{% tabs %}
{% tab title="Java" %}
```java
AdSterAdLoader.Companion.builder().withAdsListener(new MediationAdListener() {
    @Override
    public void onBannerAdLoaded(@NonNull MediationBannerAd ad) {
        super.onBannerAdLoaded(ad);
        // Show banner ad here
    }

    @Override
    public void onFailure(@NonNull AdError adError) {
        // Handle failure here
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
        // Show banner ad here
    }

    override fun onFailure(adError: AdError) {
        // Handle failure here
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

3. Inside the `onBannerAdLoaded` callback method invoke `getView()` method of `MediationnBannerAd` object to add an AdSter banner view to the given layout as shown below

```java
container.removeAllViews();
container.addView(ad.getView());
```

4. Call `MediationBannerAd.destroy()` When activity/fragment is destroyed or detached.
