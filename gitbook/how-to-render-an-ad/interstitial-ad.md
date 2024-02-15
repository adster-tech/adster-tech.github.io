---
description: Below are the steps to load and show an Interstitial ad on your app
---

# 📪 Interstitial Ad

1. Create your `AdRequestConfiguration` as per the below format

```java
val configuration = AdRequestConfiguration.Companion.builder(context, "Your_placement_name");
```

2. Call `loadAd()` method as per below format

{% tabs %}
{% tab title="Java" %}
```java
AdSterAdLoader.Companion.builder().withAdsListener(new MediationAdListener(){
    @Override
    public void onInterstitialAdLoaded(@NonNull MediationInterstitialAd ad) {
        super.onInterstitialAdLoaded(ad);
        //Show interstitial ad here
    }

    @Override
    public void onFailure(@NonNull AdError adError) {
        //Handle failure callback here
    }
}).withInterstitialAdEventsListener(new InterstitialAdEventsListener() {
    @Override
    public void onAdClicked() {
        //Handle ad click here
    }

    @Override
    public void onAdImpression() {
        //Handle ad impression here
    }

    @Override
    public void onAdOpened() {
        //Handle ad open here
    }

    @Override
    public void onAdClosed() {
        //Handle ad closed here
    }
}).build().loadAd(configuration.build());
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
AdSterAdLoader.builder().withAdsListener(object : MediationAdListener() {
    override fun onInterstitialAdLoaded(ad: MediationInterstitialAd) {
        super.onInterstitialAdLoaded(ad)
        //Show interstitial ad here
    }

    override fun onFailure(adError: AdError) {
        //Handle failure callback here
    }
}).withInterstitialAdEventsListener(object : InterstitialAdEventsListener() {
    override fun onAdClicked() {
        //Handle ad click here
    }
    override fun onAdImpression() {
        //Handle ad impression here
    }
    override fun onAdOpened() {
        //Handle ad open here
    }
    override fun onAdClosed() {
        //Handle ad close here
    }
}).build().loadAd(configuration.build())

```
{% endtab %}
{% endtabs %}

3. Inside the `onInterstitialAdLoaded` callback method invoke `showAd(activity)` method of `MediationInterstitialAd` object to show AdSter interstitial ad above any activity as shown below

{% tabs %}
{% tab title="Java" %}
```java
@Override
public void onInterstitialAdLoaded(@NonNull MediationInterstitialAd ad) {
     super.onInterstitialAdLoaded(ad);
     ad.showAd(getApplicationContext());
  }

```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
override fun onInterstitialAdLoaded (ad: MediationInterstitialAd) {
    super.onInterstitialAdLoaded (ad)
    ad.showAd(activity);
}
```
{% endtab %}
{% endtabs %}

4. Make sure to pass only Activity\`s context as parameter to `showAd()`
