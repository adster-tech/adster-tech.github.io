---
description: Below are the steps to load and show an Interstitial ad on your app
---

# 📪 Interstitial Ad

1. Create your `AdRequestConfiguration` as per the below format

```java
val configuration = AdRequestConfiguration(context,"Your_placement_name")
```

2. Call `loadAd()` method as per below format

{% tabs %}
{% tab title="Java" %}
```java
AdSter.INSTANCE.loadAd(configuration, new AdsEventListener() {
  @Override
    public void onInterstitialAdLoaded(@NonNull MediationInterstitialAd ad) {
      super.onInterstitialAdLoaded(ad);
    }

  @Override
    public void onFailure(@NonNull AdError adError) {
      // Handle Failure here
    }
});
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
AdSter.loadAd(configuration, object : AdsEventListener() {
  override fun onInterstitialAdLoaded (ad: MediationInterstitialAd) {
    super. onInterstitialAdLoaded (ad)
    // Show Interstitial ad here
  }
  override fun onFailure(adError: AdError) {
    // Handle failure here
  }
})
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
  ad.showAd(activity);
}

```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
override fun onInterstitialAdLoaded (ad: MediationInterstitialAd) {
    super. onInterstitialAdLoaded (ad)
    ad.showAd(activity);
}
```
{% endtab %}
{% endtabs %}

4. Make sure to pass only Activity\`s context as parameter to `showAd()`
