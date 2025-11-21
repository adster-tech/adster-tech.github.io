---
description: Below are the steps to load and show a rewarded ad on your app
---

# 📪 Rewarded Ad

1. Create your `AdRequestConfiguration` as per the below format

{% tabs %}
{% tab title="Java" %}
{% code overflow="wrap" %}
```java
AdRequestConfiguration.Builder configuration = AdRequestConfiguration.Companion.builder(context, "Your_placement_name");
```
{% endcode %}
{% endtab %}

{% tab title="Kotlin" %}
{% code overflow="wrap" %}
```kotlin
val configuration = AdRequestConfiguration.builder(context, "Your_placement_name")v
```
{% endcode %}
{% endtab %}
{% endtabs %}

2. Call `loadAd()` method as per below format

{% tabs %}
{% tab title="Java" %}
```java
AdSterAdLoader.Companion.builder().withAdsListener(new MediationAdListener(){
    @Override
    public void onRewardedAdLoaded(@NonNull MediationRewardedAd ad) {
        super.onRewardedAdLoaded(ad);
        //Show Rewarded ad here
    }

    @Override
    public void onFailure(@NonNull AdError adError) {
        //Handle failure callback here
    }
}).withRewardedAdEventsListener(new RewardedAdEventsListener() {
    @Override
    public void onAdClicked() {
        //Handle ad click here
    }

    @Override
    public void onAdImpression() {
        //Handle ad click here
    }

    @Override
    public void onUserEarnedReward(@NonNull Reward reward) {
        //Handle ad click here
    }

    @Override
    public void onVideoComplete() {
        //Handle ad click here
    }

    @Override
    public void onVideoClosed() {
        //Handle ad click here
    }

    @Override
    public void onVideoStart() {
        //Handle ad click here
    }
    
    @Override
    public void onAdRevenuePaid(double revenue, @NotNull String adUnitId,@NotNull String network) {
        // Callback which provides revenue and the network which provided it
    }
}).build().loadAd(configuration.build());
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
AdSterAdLoader.builder().withAdsListener(object : MediationAdListener() {
    override fun onRewardedAdLoaded(ad: MediationRewardedAd) {
        super.onRewardedAdLoaded(ad)
        //Show Rewarded ad here
    }

    override fun onFailure(adError: AdError) {
        //Handle failure callback here
    }
}).withRewardedAdEventsListener(object : RewardedAdEventsListener() {
    override fun onAdClicked() {
        //Handle ad click here
    }

    override fun onAdImpression() {
        //Handle ad click here
    }

    override fun onUserEarnedReward(reward: Reward) {
        //Handle ad click here
    }

    override fun onVideoComplete() {
        //Handle ad click here
    }

    override fun onVideoClosed() {
        //Handle ad click here
    }

    override fun onVideoStart() {
        //Handle ad click here
    }
    
    override fun onAdRevenuePaid(revenue: Double, adUnitId: String, network: String) {
        // Callback which provides revenue and the network which provided it
    }
}).build().loadAd(configuration.build())

```
{% endtab %}
{% endtabs %}

3. Inside the `onRewardedAdLoaded` callback method invoke `showAd(activity)` method of `MediationRewardedAd` object to show AdSter rewarded ad above any activity as shown below

{% tabs %}
{% tab title="Java" %}
```java
@Override
public void onRewardedAdLoaded(@NonNull MediationRewardedAd ad) {
  super.onRewardedAdLoaded(ad);
  ad.showAd(activity);
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
override fun onRewardedAdLoaded (ad: MediationRewardedAd) {
    super.onRewardedAdLoaded (ad)
    ad.showAd(activity);
}
```
{% endtab %}
{% endtabs %}

4. Make sure to pass only Activity\`s context as parameter to `showAd()`
