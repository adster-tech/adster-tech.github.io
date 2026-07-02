---
description: Below are the steps to request a collapsible anchored adaptive banner ad.
---

# 🎨 Collapsible Anchored Adaptive Banner Ad (Only for GAM)

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
val configuration = AdRequestConfiguration.builder(context, "Your_placement_name")
```
{% endcode %}
{% endtab %}
{% endtabs %}

2. Adding anchored adaptive ad type to AdRequest.

{% tabs %}
{% tab title="Java" %}
{% code overflow="wrap" %}
```java
configuration.addAnchoredAdaptiveBannerAdSize(300, CollapsiblePlacement.BOTTOM);
```
{% endcode %}
{% endtab %}

{% tab title="Kotlin" %}
{% code overflow="wrap" %}
```kotlin
configuration.addAnchoredAdaptiveBannerAdSize(320, CollapsiblePlacement.TOP)
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
The collapsible placement defines how the expanded region anchors to the banner ad.
{% endhint %}

| Placement value | Behavior                                                                | Intended use case                             |
| --------------- | ----------------------------------------------------------------------- | --------------------------------------------- |
| TOP             | The top of the expanded ad aligns to the top of the collapsed ad.       | The ad is placed at the top of the screen.    |
| BOTTOM          | The bottom of the expanded ad aligns to the bottom of the collapsed ad. | The ad is placed at the bottom of the screen. |

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
    
    @Override
    public void onAdRevenuePaid(double revenue, @NotNull String adUnitId, @NotNull String network, @NotNull String currency, @NotNull PrecisionType precisionType) {
        // Callback which provides revenue and the network which provided it
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
    
    override fun onAdRevenuePaid(revenue: Double, adUnitId: String, network: String, currency: String, precisionType: PrecisionType) {
        // Callback which provides revenue and the network which provided it
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
