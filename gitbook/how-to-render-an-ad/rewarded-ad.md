---
description: Below are the steps to load and show a rewarded ad on your app
---

# 📪 Rewarded Ad

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
    public void onRewardedAdLoaded(@NonNull MediationRewardedAd ad) {
      super.onRewardedAdLoaded(ad);
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
  override fun onRewardedAdLoaded (ad: MediationRewardedAd) {
    super. onRewardedAdLoaded (ad)
    // Show Reward ad here
  }
  override fun onFailure(adError: AdError) {
    // Handle failure here
  }
})
```
{% endtab %}
{% endtabs %}

3. Inside the `onRewardedAdLoaded` callback method invoke `showAd(activity)` method of `MediationRewardedAd` object to show AdSter rewarded ad above any activity as shown below

{% tabs %}
{% tab title="Java" %}
```java
@Override
public void onInterstitialAdLoaded(@NonNull MediationRewardedlAd ad) {
  super.onInterstitialAdLoaded(ad);
  ad.showAd(activity);
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
override fun onRewardedAdLoaded (ad: MediationRewardedAd) {
    super. onRewardedAdLoaded (ad)
    ad.showAd(activity);
}
```
{% endtab %}
{% endtabs %}

4. Make sure to pass only Activity\`s context as parameter to `showAd()`
