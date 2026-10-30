---
description: Below are the steps to load and show a custom native ad on your app
---

# 📪 Custom Native Ad

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

2. Call `loadAd()` method as per below format

{% tabs %}
{% tab title="Java" %}
```java
AdSterAdLoader.Companion.builder().withAdsListener(new MediationAdListener() {
    @Override
    public void onNativeCustomFormatAdLoaded(@NonNull MediationNativeCustomFormatAd ad) {
        super.onNativeCustomFormatAdLoaded(ad);
        if ("123456".equals(ad.getCustomFormatId())) {
            // Show native custom format for template Id 123456
        } else if ("654321".equals(ad.getCustomFormatId())) {
            // Show native custom format for template Id 654321
        }
    }

    @Override
    public void onFailure(@NonNull AdError adError) {
        //Handle failure callback here
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
    public void onAdRevenuePaid(double revenue, @NotNull String adUnitId,@NotNull String network, @NotNull String currency, @NotNull PrecisionType precisionType) {
        // Callback which provides revenue and the network which provided it
    }
}).build().loadAd(configuration.build());
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
AdSterAdLoader.builder().withAdsListener(object : MediationAdListener() {
    override fun onNativeCustomFormatAdLoaded(ad: MediationNativeCustomFormatAd) {
        super.onNativeCustomFormatAdLoaded(ad)
        //Show native custom format ad here
        if(ad.getCustomFormatId() == "123456"){
            // Show native custom format for template Id 123456
        } else if (ad.getCustomFormatId() == "654321") {
            // Show native custom format for template Id 654321
        }
    }

    override fun onFailure(adError: AdError) {
        //Handle failure callback here
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

3. Inside the `onNativeCustomFormatAdLoaded` callback method use `MediationNativeCustomFormatAd` object to display custom native ad on your defined layout.
4. Define your native ad layout, below is just an example of a layout

{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android" xmlns:app="http://schemas.android.com/apk/res-auto" android:layout_width="match_parent" android:layout_height="wrap_content" android:padding="16dp">
    
    <!-- Icon Logo -->
    <ImageView
      android:id="@+id/iconLogoImageView"
      android:layout_width="54dp"
      android:layout_height="54dp"
      android:visibility="gone"
      app:layout_constraintStart_toStartOf="parent"
      app:layout_constraintTop_toTopOf="parent"
      app:layout_constraintBottom_toBottomOf="parent"
      />
    
    <!-- choice Logo -->
    <ImageView
      android:id="@+id/choiceImageview"
      android:layout_width="20dp"
      android:layout_height="20dp"
      android:visibility="visible"
      app:layout_constraintEnd_toEndOf="parent"
      app:layout_constraintTop_toTopOf="parent"
      />
    
    <androidx.constraintlayout.widget.Guideline
        android:id="@+id/guideline"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        app:layout_constraintGuide_percent="0.2" />
    
    <!-- Title -->
    <TextView
        android:id="@+id/titleTextView"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:text="Sample Title"
        android:textSize="18sp"
        android:textStyle="bold"
        app:layout_constraintStart_toEndOf="@+id/guideline"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        />
    
    <!-- Body -->
    <TextView
        android:id="@+id/bodyTextView"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:text="Sample Body Text"
        android:textSize="14sp"
        android:layout_marginStart="8dp"
        app:layout_constraintStart_toEndOf="@+id/guideline"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/titleTextView" />
    <TextView
        android:id="@+id/infoTextView"
        android:layout_width="wrap_content"
        android:layout_height="20dp"
        android:text="Sample advertiser name"
        android:textSize="15sp"
        app:layout_constraintStart_toEndOf="@+id/guideline"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/bodyTextView" />
    
    <!-- CTA Button -->
    <Button
        android:id="@+id/ctaButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Learn More"
        app:layout_constraintStart_toEndOf="@+id/guideline"
        app:layout_constraintTop_toBottomOf="@+id/infoTextView"
        app:layout_constraintEnd_toEndOf="parent" />

    <!-- SDK video media; hidden for the image-only fallback -->
    <FrameLayout
        android:id="@+id/mediaView"
        android:layout_width="0dp"
        android:layout_height="200dp"
        android:layout_marginTop="12dp"
        android:visibility="gone"
        app:layout_constraintTop_toBottomOf="@id/ctaButton"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintBottom_toBottomOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>
```
{% endcode %}

5. The above sample layout can be used with the `MediationNativeCustomFormatAd` object to render an ad as shown in the below example

{% tabs %}
{% tab title="Java" %}
```java
private void displayNativeCustomFormatAd(MediationNativeCustomFormatAd ad){
  MediationNativeAdView adView =new MediationNativeAdView(this);
  View nativeAdView = LayoutInflater.from(this).inflate(R.layout.ad_native_layout, adView);
  TextView title = adView.findViewById(R.id.titleTextView);
  TextView body = adView.findViewById(R.id.bodyTextView);
  Button cta = adView.findViewById(R.id.ctaButton);
  ImageView logo = adView.findViewById(R.id.iconLogoImageView);
  TextView info = adView.findViewById(R.id.infoTextView);

  adView.setBodyView(body);
  adView.setHeadlineView(title);
  adView.setCtaView(cta);
  adView.setLogoView(logo);
  adView.setAdvertiserView(info);

  FrameLayout mediaContainer = adView.findViewById(R.id.mediaView);
  View media = ad.getMediaView();
  if (media != null) {
      // AdSter video: use the supplied view, including its playback controls.
      if (media.getParent() instanceof ViewGroup) {
          ((ViewGroup) media.getParent()).removeView(media);
      }
      mediaContainer.addView(media, new FrameLayout.LayoutParams(
          ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));
      mediaContainer.setVisibility(View.VISIBLE);
      logo.setVisibility(View.GONE);
  } else if (ad.getMediaContent() != null) {
      // Preserve the GAM media path; it does not use AdSterVideoController.
      com.google.android.gms.ads.nativead.MediaView googleMedia =
          new com.google.android.gms.ads.nativead.MediaView(this);
      googleMedia.setMediaContent(ad.getMediaContent());
      mediaContainer.addView(googleMedia, new FrameLayout.LayoutParams(
          ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));
      mediaContainer.setVisibility(View.VISIBLE);
      logo.setVisibility(View.GONE);
  } else {
      com.google.android.gms.ads.nativead.NativeAd.Image image = ad.getImage("Image");
      logo.setVisibility(image != null ? View.VISIBLE : View.GONE);
      if (image != null) {
          Glide.with(this).load(image.getDrawable()).into(logo);
      }
  }

  title.setText(ad.getText("Headline"));
  body.setText(ad.getText("Body"));
  cta.setText(ad.getText("Calltoaction"));
  info.setText(ad.getText("Attribution"));

  cta.setOnClickListener(new View.OnClickListener() {
    @Override
      public void onClick(View v) {
        ad.performClick("Calltoaction");
      }
  });
  
  bannerScroll.addView(nativeAdView);
  ad.trackViewability(adView);
  ad.recordImpression();
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
private fun displayNativeCustomFormatAd(ad: MediationNativeCustomFormatAd) {
  val adView = MediationNativeAdView(this)
  val nativeAdView = LayoutInflater.from(this).inflate(R.layout.ad_native_layout, adView)
  val title: TextView = adView.findViewById(R.id.titleTextView)
  val body: TextView = adView.findViewById(R.id.bodyTextView)
  val cta: Button = adView.findViewById(R.id.ctaButton)
  val logo: ImageView = adView.findViewById(R.id.iconLogoImageView)
  val info: TextView = adView.findViewById(R.id.infoTextView)

  adView.bodyView = body
  adView.headlineView = title
  adView.ctaView = cta
  adView.logoView = logo
  adView.advertiserView = info

  val mediaContainer: FrameLayout = adView.findViewById(R.id.mediaView)
  val media = ad.mediaView
  val googleContent = ad.getMediaContent()
  if (media != null) {
      // AdSter video: use the supplied view, including its playback controls.
      (media.parent as? ViewGroup)?.removeView(media)
      mediaContainer.addView(media, FrameLayout.LayoutParams(
          ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT))
      mediaContainer.visibility = View.VISIBLE
      logo.visibility = View.GONE
  } else if (googleContent != null) {
      // Preserve the GAM media path; it does not use AdSterVideoController.
      val googleMedia = com.google.android.gms.ads.nativead.MediaView(this)
      googleMedia.mediaContent = googleContent
      mediaContainer.addView(googleMedia, FrameLayout.LayoutParams(
          ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT))
      mediaContainer.visibility = View.VISIBLE
      logo.visibility = View.GONE
  } else {
      val image = ad.getImage("Image")
      logo.visibility = if (image != null) View.VISIBLE else View.GONE
      image?.let { Glide.with(this).load(it.drawable).into(logo) }
  }

  title.text = ad.getText("Headline")
  body.text = ad.getText("Body")
  cta.text = ad.getText("Calltoaction")
  info.text = ad.getText("Attribution")

  cta.setOnClickListener {
    ad.performClick("Calltoaction")
  }
  
  bannerScroll.addView(nativeAdView)
  ad.trackViewability(adView)
  ad.recordImpression()
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
For custom native ads, bind assets and click handlers before attaching the view. Call `trackViewability(adView)` and `recordImpression()` when displaying the ad, as shown above.
{% endhint %}

6. Call `MediationNativeCustomFormatAd.destroy` when activity or fragment is getting destroyed.

## Native video playback

These playback controls apply to AdSter-served native video. Keep the SDK-provided `mediaView` in your layout so the SDK can handle playback, controls, and video tracking. Image ads and other networks may return a null `videoController`; always check it. For AdSter custom native video, use `mediaView`, even when `getMediaContent()` is null. Google media content follows the separate GAM path.

### Start with sound

To start unmuted, call `unmute()` on the main thread in `onNativeCustomFormatAdLoaded`, before your display method attaches the ad view. This also works before the player finishes preparing. Apply the choice to every newly loaded ad; each starts with the muted default.

{% tabs %}
{% tab title="Java" %}
```java
// Inside onNativeCustomFormatAdLoaded(MediationNativeCustomFormatAd ad), before displaying it:
com.adster.sdk.mediation.adster.view.AdSterVideoController controller =
        ad.getVideoController();
if (controller != null) {
    controller.unmute(); // Optional: omit this to keep the muted default.
}
// Now call your display method to bind and attach the ad.
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
// Inside onNativeCustomFormatAdLoaded(ad: MediationNativeCustomFormatAd), before displaying it:
ad.videoController?.unmute() // Optional: omit this to keep the muted default.
// Now call your display method to bind and attach the ad.
```
{% endtab %}
{% endtabs %}

### Control playback

Use `com.adster.sdk.mediation.adster.view.AdSterVideoController` on the main thread. Each method below is an independent action for your UI; do not call them all in sequence.

| API                              | Behavior                                                                               |
| -------------------------------- | -------------------------------------------------------------------------------------- |
| `play()`                         | Resumes a paused video when the view can play.                                         |
| `pause()`                        | Pauses playback until `play()` is called or the viewer resumes using the SDK controls. |
| `mute()` / `unmute()`            | Changes sound immediately, or stores the choice until preparation finishes.            |
| `isPlaying` / Java `isPlaying()` | Reports whether the player is currently playing.                                       |
| `isMuted` / Java `isMuted()`     | Reports the current mute setting.                                                      |

{% tabs %}
{% tab title="Java" %}
```java
com.adster.sdk.mediation.adster.view.AdSterVideoController controller =
        ad.getVideoController();
if (controller != null) {
    controller.pause(); // For example, when your app explicitly pauses this ad.
}
// Later, when your app wants to resume:
// if (controller != null) controller.play();
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
ad.videoController?.pause() // For example, when your app explicitly pauses this ad.
// Later, when your app wants to resume:
// ad.videoController?.play()
```
{% endtab %}
{% endtabs %}

### Lifecycle and cleanup

Retain the loaded ad object and call `destroy()` when replacing it or permanently removing it, including Activity destruction or Fragment `onDestroyView()`. Remove its view and clear your reference. Do not destroy an ad for a temporary pause if you intend to resume it.

{% tabs %}
{% tab title="Java" %}
```java
// When permanently removing the ad (ad is the retained MediationNativeCustomFormatAd):
ad.destroy();
// Remove its view from your container and clear your retained ad reference.
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
// When permanently removing the ad (ad is the retained MediationNativeCustomFormatAd):
ad.destroy()
// Remove its view from your container and clear your retained ad reference.
```
{% endtab %}
{% endtabs %}
