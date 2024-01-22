---
description: Below are the steps to load and render a banner Ad on your app
---

# 📪 Banner Ad

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
    public void onBannerAdLoaded(@NonNull MediationBannerAd ad) {
      super.onBannerAdLoaded(ad);
      // Show banner ad here
    }
  @Override
    public void onFailure(@NonNull AdError adError) {
      super.onFailure(adError);
      // Handle failure here
    }
});
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
AdSter.loadAd(configuration, object : AdsEventListener() {
  override fun onBannerAdLoaded(ad: MediationBannerAd) {
    super.onBannerAdLoaded(ad)
    // Show banner ad here
  }
  override fun onFailure(adError: AdError) {
    // Handle failure here
  }
});
```
{% endtab %}
{% endtabs %}

3. Inside the `onBannerAdLoaded` callback method invoke `getView()` method of `MediationnBannerAd` object to add an AdSter banner view to the given layout as shown below

```java
container.removeAllViews();
container.addView(ad.getView());
```

4. Call `MediationBannerAd.destroy()` When activity/fragment is destroyed or detached.
