---
description: Below are the steps to load and show a native ad on your app
---

# 📪 Video ad

1. Create your `AdRequestConfiguration` as per the below format

```java
val configuration = AdRequestConfiguration.Companion.builder(context, "Your_placement_name");
```

2. Set `mediaController` and `audioManger` along with instantiation of `videoView` and `videoPlayerContainer`

{% tabs %}
{% tab title="Java" %}
<pre class="language-java"><code class="lang-java">private VideoView videoView;
private int savedPosition = 0;
<strong>videoView = (VideoView) findViewById(R.id.videoView);
</strong>String videoUrl = "Your Video URL";

// Create a MediaController and set it as the controller for the VideoView
MediaController mediaController = new MediaController(this);
mediaController.setAnchorView(videoView);
mediaController.setMediaPlayer(videoView);
videoView.setMediaController(mediaController);

// Initialize the AudioManager
AudioManager audioManager = (AudioManager) getSystemService(AUDIO_SERVICE);
FrameLayout videoPlayerContainer = (FrameLayout) findViewById(R.id.mainVideo);

videoView.setVideoURI(Uri.parse(videoUrl));
videoView.requestFocus();
videoView.start();
</code></pre>
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val videoView = findViewById(R.id.videoView)
val videoUrl = "Your Video URL"

// Create a MediaController and set it as the controller for the VideoView
val mediaController = MediaController(this)
mediaController.setAnchorView(videoView)
mediaController.setMediaPlayer(videoView)
videoView.setMediaController(mediaController)
// Initialize the AudioManager
val audioManager = getSystemService(AUDIO_SERVICE) as AudioManager
val videoPlayerContainer = findViewById<FrameLayout>(R.id.mainVideo)
videoView.setVideoURI(Uri.parse(videoUrl))
videoView.requestFocus()
videoView.start()
var savedPosition = 0
```
{% endtab %}
{% endtabs %}

3. Call `loadVideoAd()` method as per below format

{% tabs %}
{% tab title="Java" %}
```java
AdSter.INSTANCE.loadVideoAd(
getApplicationContext(), "Your description URL", videoPlayerContainer, videoView, mediaController, audioManager, 
    AdRequestConfiguration.Companion.builder(
    getApplicationContext(), "Your Placement Id").build(), new VideoAdEventsListener() {
    @Override
    public void onAdLoaded() {
        super.onAdLoaded();
        savedPosition = videoView.getCurrentPosition();
    }

    @Override
    public void onAdPaused() {
        super.onAdPaused();
    }

    @Override
    public void onAdTapped() {
        super.onAdTapped();
    }

    @Override
    public void onAdPlayed() {
        super.onAdPlayed();
    }

    @Override
    public void onAdStopped() {
        super.onAdStopped();
    }

    @Override
    public void onVolumeChanged(int volumeDelta) {
        super.onVolumeChanged(volumeDelta);
    }

    @Override
    public void onAllAdCompleted() {
        super.onAllAdCompleted();
        mediaController.setAnchorView(videoView);
        videoView.setMediaController(mediaController);
        videoView.setVideoURI(Uri.parse(videoUrl));
        videoView.requestFocus();
        videoView.setOnPreparedListener(new MediaPlayer.OnPreparedListener() {
            @Override
            public void onPrepared(MediaPlayer mp) {
                if (savedPosition > 0) {
                    videoView.seekTo(savedPosition);
                }
                videoView.start();
            }
        });
    }

    @Override
    public void onContentPauseRequested() {
        super.onContentPauseRequested();
    }

    @Override
    public void onContentResumeRequested() {
        super.onContentResumeRequested();
    }

    @Override
    public void onAdClicked() {
        super.onAdClicked();
        mediaController.show(3000);
    }

    @Override
    public void onAdLoadFailure(@NonNull AdError adError) {
        super.onAdLoadFailure(adError);
    }
});
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
AdSter.INSTANCE.loadVideoAd(
    applicationContext, "Your description URL", videoPlayerContainer, videoView, mediaController, audioManager, 
    AdRequestConfiguration.builder(
        applicationContext, "Your Placement Id"
    ).build(), object : VideoAdEventsListener() {
        override fun onAdLoaded() {
            super.onAdLoaded()
            savedPosition = videoView.currentPosition
        }

        override fun onAdPaused() {
            super.onAdPaused()
        }

        override fun onAdTapped() {
            super.onAdTapped()
        }

        override fun onAdPlayed() {
            super.onAdPlayed()
        }

        override fun onAdStopped() {
            super.onAdStopped()
        }

        override fun onVolumeChanged(volumeDelta: Int) {
            super.onVolumeChanged(volumeDelta)
        }

        override fun onAllAdCompleted() {
            super.onAllAdCompleted()
            mediaController.setAnchorView(videoView)
            videoView.setMediaController(mediaController)
            videoView.setVideoURI(Uri.parse(videoUrl))
            videoView.requestFocus()
            videoView.setOnPreparedListener { mp ->
                if (savedPosition > 0) {
                    videoView.seekTo(savedPosition)
                }
                videoView.start()
            }
        }

        override fun onContentPauseRequested() {
            super.onContentPauseRequested()
        }

        override fun onContentResumeRequested() {
            super.onContentResumeRequested()
        }

        override fun onAdClicked() {
            super.onAdClicked()
            mediaController.show(3000)
        }

        override fun onAdLoadFailure(adError: AdError) {
            super.onAdLoadFailure(adError)
        }
    }
)

```
{% endtab %}
{% endtabs %}

4. After the `loadVideoAd()`, call `showVideoAdIfAvailable()` to display a video ad.&#x20;

{% tabs %}
{% tab title="Java" %}
```java
AdSter.INSTANCE.showVideoAdIfAvailable(getApplicationContext(), "Your description URL", videoPlayerContainer, videoView, mediaController, audioManager, AdRequestConfiguration.Companion.builder(getApplicationContext(), "Home_Screen_Video").build(), new VideoAdEventsListener() {
    @Override
    public void onAdLoaded() {
        super.onAdLoaded();
        savedPosition = videoView.getCurrentPosition();
    }

    @Override
    public void onAdPaused() {
        super.onAdPaused();
    }

    @Override
    public void onAdPlayed() {
        super.onAdPlayed();
    }

    @Override
    public void onAdTapped() {
        super.onAdTapped();
    }

    @Override
    public void onAdStopped() {
        super.onAdStopped();
    }

    @Override
    public void onVolumeChanged(int volumeDelta) {
        super.onVolumeChanged(volumeDelta);
    }

    @Override
    public void onAllAdCompleted() {
        super.onAllAdCompleted();

        mediaController.setAnchorView(videoView);

        videoView.setMediaController(mediaController);
        videoView.setVideoURI(Uri.parse(videoUrl));
        videoView.requestFocus();

        videoView.setOnPreparedListener(new MediaPlayer.OnPreparedListener() {
            @Override
            public void onPrepared(MediaPlayer mp) {
                if (savedPosition > 0) {
                    videoView.seekTo(savedPosition);
                }
                videoView.start();
            }
        });
    }

    @Override
    public void onContentPauseRequested() {
        super.onContentPauseRequested();
    }

    @Override
    public void onContentResumeRequested() {
        super.onContentResumeRequested();
    }

    @Override
    public void onAdClicked() {
        super.onAdClicked();
        mediaController.show(3000);
    }

    @Override
    public void onAdLoadFailure(@NonNull AdError adError) {
        super.onAdLoadFailure(adError);
    }
});
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
AdSter.INSTANCE.showVideoAdIfAvailable(applicationContext, "Your description URL", videoPlayerContainer, videoView, mediaController, audioManager, 
    AdRequestConfiguration.builder(
        applicationContext, 
        "Your Placement Id"
    ).build(),
    object : VideoAdEventsListener() {
        override fun onAdLoaded() {
            super.onAdLoaded()
            savedPosition = videoView.currentPosition
        }

        override fun onAdPaused() {
            super.onAdPaused()
        }

        override fun onAdPlayed() {
            super.onAdPlayed()
        }

        override fun onAdTapped() {
            super.onAdTapped()
        }

        override fun onAdStopped() {
            super.onAdStopped()
        }

        override fun onVolumeChanged(volumeDelta: Int) {
            super.onVolumeChanged(volumeDelta)
        }

        override fun onAllAdCompleted() {
            super.onAllAdCompleted()
            addTextViewToParent(videoDes, "onAllAdCompleted")

            mediaController.setAnchorView(videoView)
            videoView.setMediaController(mediaController)
            videoView.setVideoURI(Uri.parse(videoUrl))
            videoView.requestFocus()

            videoView.setOnPreparedListener { mp ->
                if (savedPosition > 0) {
                    videoView.seekTo(savedPosition)
                }
                videoView.start()
            }
        }

        override fun onContentPauseRequested() {
            super.onContentPauseRequested()
        }

        override fun onContentResumeRequested() {
            super.onContentResumeRequested()
        }

        override fun onAdClicked() {
            super.onAdClicked()
            mediaController.show(3000)
        }

        override fun onAdLoadFailure(adError: AdError) {
            super.onAdLoadFailure(adError)
        }
    }
)

```
{% endtab %}
{% endtabs %}
