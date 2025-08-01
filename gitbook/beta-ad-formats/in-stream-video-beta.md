# 🎨 In-stream Video (Beta)

AdSter SDK also gives the option to load and show in-stream video ad format which is the proprietary Ad format of IMA SDK.&#x20;

Create your `AdRequestConfiguration` as per the below format

{% code overflow="wrap" %}
```java
AdRequestConfiguration configuration = AdRequestConfiguration.Companion
    .builder(context, "Your_placement_name")
    .addVideoPlayer(playerView, audioManager)
    .setContentUrl("https://your-video-url.mp4")
    .build();

```
{% endcode %}

## Load and show In-stream Video Ad

Call `loadAd()` method as per below format

{% tabs %}
{% tab title="Java" %}
{% code fullWidth="true" %}
```java
AdSterAdLoader.Companion.builder()
    .withAdsListener(new MediationAdListener() {
        @Override
        public void onVideoAdLoaded(@NonNull MediationVideoAd ad) {
            Log.d("AdCallback", "Ad Loaded");
        }

        @Override
        public void onFailure(@NonNull AdError error) {
            Log.e("AdCallback", "Ad Load Failed: " + error.getErrorMessage());
        }
    })
    .withVideoAdEventsListener(new VideoAdEventsListener() {
        @Override public void onAdPlayed() {}
        @Override public void onAdSkipped() {}
        @Override public void onAdStopped() {}
        @Override public void onAllAdCompleted() {}
        @Override public void onContentPauseRequested() {}
        @Override public void onContentResumeRequested() {}
        @Override public void onAdLoadFailure(@NonNull AdError error) {}
        @Override public void onAdClicked() {}
        @Override public void onVolumeChanged(int delta) {}
        @Override public void onAdTapped() {}
        @Override public void onAdPaused() {}
        @Override public void onSkippableStateChanged() {}
    })
    .build()
    .loadAd(configuration);
```
{% endcode %}
{% endtab %}

{% tab title="Kotlin" %}
{% code overflow="wrap" fullWidth="false" %}
```kotlin
AdSterAdLoader.builder()
    .withAdsListener(object : MediationAdListener {
        override fun onVideoAdLoaded(ad: MediationVideoAd) {
            Log.d("AdCallback", "Ad Loaded")
        }

        override fun onFailure(error: AdError) {
            Log.e("AdCallback", "Ad Load Failed: ${error.errorMessage}")
        }
    })
    .withVideoAdEventsListener(object : VideoAdEventsListener() {
        override fun onAdPlayed() {}
        override fun onAdSkipped() {}
        override fun onAdStopped() {}
        override fun onAllAdCompleted() {}
        override fun onContentPauseRequested() {}
        override fun onContentResumeRequested() {}
        override fun onAdLoadFailure(error: AdError) {}
        override fun onAdClicked() {}
        override fun onVolumeChanged(volumeDelta: Int) {}
        override fun onAdTapped() {}
        override fun onAdPaused() {}
        override fun onSkippableStateChanged() {}
    })
    .build()
    .loadAd(configuration)
```
{% endcode %}
{% endtab %}
{% endtabs %}

{% hint style="success" %}
Reference for sample implementation\
[https://storage.googleapis.com/adster-unity-bridge-docs/in-stream-ads/AdActivityVideo.java](https://storage.googleapis.com/adster-unity-bridge-docs/in-stream-ads/AdActivityVideo.java)\
[https://storage.googleapis.com/adster-unity-bridge-docs/in-stream-ads/activity\_ad\_video.xml](https://storage.googleapis.com/adster-unity-bridge-docs/in-stream-ads/activity_ad_video.xml)
{% endhint %}
