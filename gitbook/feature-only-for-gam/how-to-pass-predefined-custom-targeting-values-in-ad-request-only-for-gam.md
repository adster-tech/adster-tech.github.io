---
description: >-
  Below are the steps to pass predefined custom targeting value in ad request
  for GAM (Supported by all ad formats)
---

# 🎨 How to pass predefined custom targeting values in ad request (Only for GAM)

1. Create your `AdRequestConfiguration` as per the below format

{% code overflow="wrap" %}
```java
val configuration = AdRequestConfiguration.Companion.builder(context, "Your_placement_name");
```
{% endcode %}

2. Adding predefined ad targeting parameters to AdRequest

<details>

<summary>Single key with single value</summary>

```java
configuration.addCustomTargetingValue("YOUR_KEY","YOUR_VALUE")
```

</details>

<details>

<summary>Single key with multiple values</summary>

```java
configuration.addCustomTargetingValue("YOUR_KEY",List<String>)
```

</details>

<details>

<summary>Multiple keys with single value</summary>

```java
configuration.addCustomTargetingValue("YOUR_KEY","YOUR_VALUE")
             .addCustomTargetingValue("YOUR_KEY","YOUR_VALUE")
```

</details>

<details>

<summary>Multiple keys with multiple values</summary>

```java
configuration.addCustomTargetingValue("YOUR_KEY",List<String>)
             .addCustomTargetingValue("YOUR_KEY",List<String>)
```

</details>

{% hint style="info" %}
#### Custom ad request can be created for all the ad types.

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
