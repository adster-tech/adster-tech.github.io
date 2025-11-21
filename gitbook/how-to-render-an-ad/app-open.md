# 📪 App Open

AdSter SDK also gives the option to load and show AppOpen ad format which is the proprietary Ad format of Google Ad Manager and AdMob. Implementation is similar to that given in this document [https://developers.google.com/admob/android/app-open](https://developers.google.com/admob/android/app-open). Instead of creating a new `AppOpenAdManager` mentioned in the document use the method below provided by AdSter SDK and follow the implementation on the Activity and Application class just like the document. AdSter SDK provides methods to show and load app-open ads

Create your `AdRequestConfiguration` as per the below format

{% tabs %}
{% tab title="Java" %}
{% code overflow="wrap" expandable="true" %}
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

## Load App Open Ad

Call `loadAd()` method as per below format

{% tabs %}
{% tab title="Java" %}
```java
AdSterAdLoader.Companion.builder().withAdsListener(new MediationAdListener() {
    @Override
    public void onFailure(@NonNull AdError adError) {
        //Handle failure callback here
    }

    @Override
    public void onAppOpenAdLoaded(@NonNull MediationAppOpenAd ad) {
        super.onAppOpenAdLoaded(ad);
        //Show App Open Ad here
    }
}).withAppOpenAdEventsListener(new AppOpenAdEventsListener() {
    @Override
    public void onAdClicked() {
        // Callback when ad is clicked
    }

    @Override
    public void onAdImpression() {
        // Callback when ad is shown
    }

    @Override
    public void onAdOpened() {
        // Callback when ad is opened
    }

    @Override
    public void onAdClosed() {
        // Callback when ad is cloed
    }

    @Override
    public void onFailure(@Nullable AdError adError) {
        // Callback when there is failure
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
AdSterAdLoader.builder().withAdsListener(object : MediationAdListener(){
    override fun onAppOpenAdLoaded(ad: MediationAppOpenAd) {
        super.onAppOpenAdLoaded(ad)
        // Show App Open Ad here
    }
    override fun onFailure(adError: AdError) {
        //Handle failure callback here
    }

}).withAppOpenAdEventsListener(object : AppOpenAdEventsListener(){
    override fun onAdClicked() {
        // Handle Ad clicked here
    }

    override fun onAdClosed() {
        // Handle Ad closed here
    }

    override fun onAdImpression() {
        // Handle Ad impression here
    }

    override fun onAdOpened() {
        // Handle Ad Open here
    }

    override fun onFailure(adError: AdError?) {
        // Handle Ad Failure here
    }
    
    override fun onAdRevenuePaid(revenue: Double, adUnitId: String, network: String) {
        // Callback which provides revenue and the network which provided it
    }
}).build().loadAd(configuration.build())
```
{% endtab %}
{% endtabs %}

***

## Show AppOpen Ad

Inside the `onAppOpenAdLoaded` callback method invoke `showAd(activity)` method of `MediationAppOpenAd` object to show AdSter App Open ad above any activity as shown below

{% tabs %}
{% tab title="Java" %}
{% code overflow="wrap" %}
```java
@Override
public void onAppOpenAdLoaded(@NonNull MediationAppOpenAd ad) {
    super.onAppOpenAdLoaded(ad);
    ad.showAd(activity);
}
```
{% endcode %}
{% endtab %}

{% tab title="Kotlin" %}
<pre class="language-kotlin" data-overflow="wrap"><code class="lang-kotlin">override fun onAppOpenAdLoaded(ad: MediationAppOpenAd) {
<strong>    super.onAppOpenAdLoaded(ad)
</strong>    ad.showAd(activity)
}
</code></pre>
{% endtab %}
{% endtabs %}
