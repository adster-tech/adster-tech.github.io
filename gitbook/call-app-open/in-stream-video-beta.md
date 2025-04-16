# 🎨 In-stream Video (Beta)

AdSter SDK also gives the option to load and show in-stream video ad format which is the proprietary Ad format of IMA SDK.&#x20;

Create your `AdRequestConfiguration` as per the below format

<pre class="language-java" data-overflow="wrap"><code class="lang-java"><strong>val configuration = AdRequestConfiguration.Companion.builder(context, "Your_placement_name").addVideoPlayer(VIEWGROUP, EXOPLAYER_PlayerView, AudioManager);
</strong></code></pre>

## Load and show In-stream Video Ad

Call `loadAd()` method as per below format

{% tabs %}
{% tab title="Java" %}
{% code fullWidth="true" %}
```java
    AdSterAdLoader.Companion.builder().withAdsListener(new MediationAdListener() {
        @Override
        public void onVideoAdLoaded (@NonNull MediationVideoAd ad){
        }

        @Override
        public void onFailure (@NonNull AdError adError){
        }
    }).withVideoAdEventsListener(new VideoAdEventsListener() {
        @Override
        public void onAdPaused () {
        }

        @Override
        public void onAdPlayed () {
        }

        @Override
        public void onAdStopped () {
        }

        @Override
        public void onAdSkipped () {
        }

        @Override
        public void onVolumeChanged ( int volumeDelta){
        }

        @Override
        public void onAllAdCompleted () {
        }

        @Override
        public void onContentPauseRequested () {
        }

        @Override
        public void onContentResumeRequested () {
        }

        @Override
        public void onAdClicked () {
        }

        @Override
        public void onAdLoadFailure (@NonNull AdError adError){
        }

        @Override
        public void onAdTapped () {
        }

        @Override
        public void onSkippableStateChanged () {
        }
    }).build().loadAd(configuration.build());
```
{% endcode %}
{% endtab %}

{% tab title="Kotlin" %}
{% code overflow="wrap" fullWidth="false" %}
```kotlin
AdSterAdLoader.builder().withAdsListener(object : MediationAdListener() {
    override fun onVideoAdLoaded(ad: MediationVideoAd) {
    }

    override fun onFailure(adError: AdError) {
    }
}).withVideoAdEventsListener(object : VideoAdEventsListener() {
    override fun onAdPaused() {
    }

    override fun onAdPlayed() {
    }

    override fun onAdStopped() {
    }

    override fun onAdSkipped() {
    }

    override fun onVolumeChanged(volumeDelta: Int) {
    }

    override fun onAllAdCompleted() {
    }

    override fun onContentPauseRequested() {
    }

    override fun onContentResumeRequested() {
    }

    override fun onAdClicked() {
    }

    override fun onAdLoadFailure(adError: AdError) {
    }

    override fun onAdTapped() {
    }

    override fun onSkippableStateChanged() {
    }
}).build().loadAd(configuration.build())
```
{% endcode %}
{% endtab %}
{% endtabs %}
