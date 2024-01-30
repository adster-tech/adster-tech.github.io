# 🎨 App open (Beta)

AdSter SDK also gives the option to load and show AppOpen ad format which is the proprietary Ad format of Google Ad Manager and AdMob. Implementation is similar to that given in this document [https://developers.google.com/admob/android/app-open](https://developers.google.com/admob/android/app-open). Instead of creating a new `AppOpenAdManager` mentioned in the document use the method below provided by AdSter SDK and follow the implementation on the Activity and Application class just like the document. AdSter SDK provides methods to show and load app-open ads



## Load App Open Ad

Pass the activity\`s context and your placement name as arguments to `loadAppOpenAd` method

{% tabs %}
{% tab title="Java" %}
{% code overflow="wrap" %}
```java
AdSter.INSTANCE.loadAppOpenAd(activity, new AdRequestConfiguration(activity, "Your_placement"), new AppOpenAdEventsListener() {
  @Override
    public void onAdLoaded() {
      super.onAdLoaded();
      // Here ad can be shown using a call to showAdIfAvailable method
    }

  @Override
    public void onAdLoadFailure(@NonNull AdError adError) {
      super.onAdLoadFailure(adError);
    }
});
```
{% endcode %}
{% endtab %}

{% tab title="Kotlin" %}
{% code overflow="wrap" %}
```kotlin
AdSter.loadAppOpenAd(
  activity,
  AdRequestConfiguration(activity, "Your_placement"),
  object : AppOpenAdEventsListener() {
    override fun onAdLoaded() {
        super.onAdLoaded()
        // Here ad can be shown using a call to showAdIfAvailable method
    }

    override fun onAdLoadFailure(adError: AdError) {
        super.onAdLoadFailure(adError)
    }
})
```
{% endcode %}
{% endtab %}
{% endtabs %}

***

## Show AppOpen Ad

Pass the activity\`s context and your placement name as arguments to `loadAppOpenAd` method.

{% tabs %}
{% tab title="Java" %}
{% code overflow="wrap" %}
```java
AdSter.INSTANCE.showAdIfAvailable(activity, new AdRequestConfiguration(activity, "your_placement_id"), new AppOpenAdEventsListener() {
  @Override
    public void onShowAdComplete() {
      super.onShowAdComplete();
    }

  @Override
    public void onAdLoadFailure(@NonNull AdError adError) {
      super.onAdLoadFailure(adError);
    }
});
```
{% endcode %}
{% endtab %}

{% tab title="Kotlin" %}
{% code overflow="wrap" %}
```kotlin
AdSter.showAdIfAvailable(
  activity,
  AdRequestConfiguration(activity, "your_placement_id"),
  object : AppOpenAdEventsListener() {
    override fun onShowAdComplete() {
      super.onShowAdComplete()
    }
    fun onAdLoadFailure(adError: AdError?) {
      super.onAdLoadFailure(adError!!)
    }
});
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="info" %}
This method will try to show an app open ad if already available. If not, it calls `loadAd` internally to load an app-open ad and wherever a new app-open event occurs this method immediately shows the ad.
{% endhint %}
