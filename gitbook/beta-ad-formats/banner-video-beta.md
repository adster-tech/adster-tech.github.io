# 🎨 Banner Video (Beta)

AdSter SDK also gives the option to load and show in-stream video ad in a banner format.&#x20;

Create your `AdRequestConfiguration` as per the below format

<pre class="language-java" data-overflow="wrap"><code class="lang-java"><strong>val configuration = AdRequestConfiguration.Companion.builder(context, "Your_placement_name");
</strong></code></pre>

## Load and show Banner Video Ad

Call `loadAd()` method as per below format

{% tabs %}
{% tab title="Java" %}
{% code fullWidth="true" %}
```java
AdSterAdLoader.Companion.builder().withAdsListener(new MediationAdListener() {
    @Override
    public void onBannerVideoAdLoaded (@NonNull MediationBannerVideoAd ad){ 
        //Use the ad object provided here to display the ad
    }

    @Override
    public void onFailure (@NonNull AdError adError){ }
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
    public void onAdRevenuePaid(double revenue, @NotNull String adUnitId,@NotNull String network) {
        // Callback which provides revenue and the network which provided it
    }
}).build().loadAd(configuration.build());
```
{% endcode %}
{% endtab %}

{% tab title="Kotlin" %}
<pre class="language-kotlin" data-overflow="wrap" data-full-width="false"><code class="lang-kotlin"><strong>AdSterAdLoader.builder().withAdsListener(object : MediationAdListener() {
</strong>    override fun onBannerVideoAdLoaded(ad: MediationBannerVideoAd) {
        //Use the ad object provided here to display the ad
    }

    override fun onFailure(adError: AdError) { }
}).withBannerVideoAdEventsListener(object : VideoAdEventsListener() {
    override fun onAdPaused() { }

    override fun onAdPlayed() { }
    
    override fun onAdResumed() { }

    override fun onAdStopped() { }

    override fun onAdSkipped() { }

    override fun onVolumeChanged(volumeDelta: Int) { }

    override fun onAllAdCompleted() { }

    override fun onContentPauseRequested() { }

    override fun onContentResumeRequested() { }

    override fun onAdClicked() { }

    override fun onAdLoadFailure(adError: AdError) { }

    override fun onAdTapped() { }

    override fun onSkippableStateChanged() { }
}).build().loadAd(configuration.build())
</code></pre>
{% endtab %}
{% endtabs %}

Also use the `pause()`,`resume()` and `destroy()` functions of the ad object provided in `onBannerVideoAdLoaded(MediationBannerVideoAd ad)` to pause , resume and destroy the video when the fragment or the activity is being paused , resumed and destroyed respectively.\
\
Below is an example :

{% tabs %}
{% tab title="Java" %}
```java
private MediationBannerVideoAd bannerVideoAd = null;

@Override
protected void onPause() {
    super.onPause();
    if (bannerVideoAd != null) {
        bannerVideoAd.pause();
    }
}

@Override
protected void onResume() {
    super.onResume();
    if (bannerVideoAd != null) {
        bannerVideoAd.resume();
    }
}

@Override
protected void onDestroy() {
    super.onDestroy();
    if (bannerVideoAd != null) {
        bannerVideoAd.destroy();
    }
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
private var bannerVideoAd : MediationBannerVideoAd? = null

override fun onPause() {
    super.onPause()
    bannerVideoAd?.pause()
}
    
override fun onResume() {
    super.onResume()
    bannerVideoAd?.resume()
}
    
override fun onDestroy() {
    super.onDestroy()
    bannerVideoAd?.destroy()
}
```
{% endtab %}
{% endtabs %}
