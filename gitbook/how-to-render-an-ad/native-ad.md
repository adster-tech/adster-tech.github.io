---
description: Below are the steps to load and show a native ad on your app
---

# 📪 Native Ad

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
    public void onNativeAdLoaded(@NonNull MediationNativeAd ad) {
        super.onNativeAdLoaded(ad);
        //Show native ad here
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
    override fun onNativeAdLoaded(ad: MediationNativeAd) {
        super.onNativeAdLoaded(ad)
        //Show native ad here
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

3. Inside the `onNativeAdLoaded` callback method use `MediationNativeAd` object to display native ad on your defined layout.
4. Define your native ad layout, below is just an example of a layout

{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/main"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@color/white">

    <!-- Choice Logo -->
    <ImageView
        android:id="@+id/choiceImageview"
        android:layout_width="20dp"
        android:layout_height="20dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent" />

    <LinearLayout
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:orientation="horizontal"
        android:weightSum="10"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent">

        <!-- Media View -->
        <FrameLayout
            android:id="@+id/mediaView"
            android:layout_width="0dp"
            android:layout_height="160dp"
            android:layout_weight="6" />

        <LinearLayout
            android:id="@+id/textLayout"
            android:layout_width="0dp"
            android:layout_height="match_parent"
            android:layout_marginStart="8dp"
            android:layout_marginTop="8dp"
            android:layout_marginEnd="16dp"
            android:layout_weight="4"
            android:orientation="vertical">

            <!-- Title -->
            <TextView
                android:id="@+id/titleTextView"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:ellipsize="end"
                android:maxLines="2"
                android:text="Sample Title"
                android:textColor="@color/black"
                android:textSize="16sp"
                android:textStyle="bold"
                android:visibility="gone"
                tools:visibility="visible" />

            <!-- Body -->
            <TextView
                android:id="@+id/bodyTextView"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:ellipsize="end"
                android:maxLines="2"
                android:text="Sample Body Text"
                android:textColor="@color/black"
                android:textSize="14sp"
                android:visibility="gone"
                tools:visibility="visible" />

            <!-- Info -->
            <TextView
                android:id="@+id/infoTextView"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:textColor="@color/black"
                android:textSize="12sp"
                android:visibility="gone"
                tools:text="Sample Advertiser Text"
                tools:visibility="visible" />

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:orientation="horizontal">

                <!-- Icon Logo -->
                <ImageView
                    android:id="@+id/iconLogoImageView"
                    android:layout_width="32dp"
                    android:layout_height="32dp"
                    android:scaleType="centerInside" />

                <!-- Rating Bar -->
                <RatingBar
                    android:id="@+id/ratingBar"
                    style="@style/Widget.AppCompat.RatingBar.Small"
                    android:layout_width="wrap_content"
                    android:layout_height="wrap_content"
                    android:layout_gravity="center_vertical"
                    android:lines="1"
                    android:numStars="5"
                    android:stepSize="0.1" />
            </LinearLayout>

            <!-- CTA Button -->
            <Button
                android:id="@+id/ctaButton"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:text="Learn More" />
        </LinearLayout>
    </LinearLayout>
</androidx.constraintlayout.widget.ConstraintLayout>
```
{% endcode %}

5. The above sample layout can be used with the `MediationNativeAd` object to render an ad as shown in the below example

{% tabs %}
{% tab title="Java" %}
```java
private void displayNativeAd(MediationNativeAd ad) {
  // Create AdSter MediationNativeAdView object
  MediationNativeAdView adView = new MediationNativeAdView(this);

  // Add this layout as a parent to your native ad layout
  View nativeAdView = LayoutInflater.from(this).inflate(R.layout.ad_native_layout, adView, true);

  // Set native elements
  TextView title = adView.findViewById(R.id.titleTextView);
  TextView body = adView.findViewById(R.id.bodyTextView);
  Button cta = adView.findViewById(R.id.ctaButton);
  ImageView logo = adView.findViewById(R.id.iconLogoImageView);
  ImageView choice = adView.findViewById(R.id.choiceImageview);
  TextView info = adView.findViewById(R.id.infoTextView);
  RatingBar ratingBar = adView.findViewById(R.id.ratingBar);
  // MediaView
  FrameLayout mediaView = nativeAdView.findViewById(R.id.mediaView);

  // Read once: the SDK media view renders either image or video content.
  View media = ad.getMediaView();
  if (media != null) {
      if (media.getParent() instanceof ViewGroup) {
          ((ViewGroup) media.getParent()).removeView(media);
      }
      mediaView.removeAllViews();
      mediaView.addView(media, new FrameLayout.LayoutParams(
          ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT));
      adView.setMediaView(media);
  }
  adView.setBodyView(body);
  adView.setHeadlineView(title);
  adView.setCtaView(cta);
  adView.setLogoView(logo);
  adView.setAdvertiserView(info);
  adView.setRatingBarView(ratingBar);

  logo.setVisibility(View.VISIBLE);
  // Load logo url using any Image loading library (Glide is just an example here)
  Glide.with(getApplicationContext()).load(ad.getLogo()).into(logo);

  // Set native ad elements with data
  title.setText(ad.getHeadLine());
  body.setText(ad.getBody());
  title.setVisibility(View.VISIBLE);
  body.setVisibility(View.VISIBLE);
  info.setVisibility(View.VISIBLE);
  if(ad.getStarRating()!=null){
    ratingBar.setRating(ad.getStarRating().floatValue());
  }
  cta.setText(ad.getCallToAction());
  info.setText(ad.getAdvertiser());

  Map<String, View> map = new HashMap<>();
  map.put("headline", title);
  map.put("body", body);
  map.put("cta", cta);
  map.put("advertiser",info);
  // Send views to AdSter sdk for tracking click/impressionn etc.
  ad.trackViews(adView, null, map);
  // Set MediationNativeAd object
  adView.setNativeAd(ad);
  // Ad native ad view to container
  container.removeAllViews();
  container.addView(adView);
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
private fun displayNativeAd(ad: MediationNativeAd) {
  // Create AdSter MediationNativeAdView object
  val adView = MediationNativeAdView(this)
  // Add this layout as a parent to your native ad layout
  val nativeAdView: View = LayoutInflater.from(this).inflate(R.layout.ad_native_layout, adView, true)
  // Set native elements
  val title: TextView = adView.findViewById(R.id.titleTextView)
  val body: TextView = adView.findViewById(R.id.bodyTextView)
  val cta: Button = adView.findViewById(R.id.ctaButton)
  val logo: ImageView = adView.findViewById(R.id.iconLogoImageView)
  val choice: ImageView = adView.findViewById(R.id.choiceImageview)
  val info: TextView = adView.findViewById(R.id.infoTextView)
  val ratingBar : RatingBar = adView.findViewById(R.id.ratingBar)
  // MediaView
  val mediaView: FrameLayout = nativeAdView.findViewById(R.id.mediaView)

  // Read once: the SDK media view renders either image or video content.
  val media = ad.mediaView
  if (media != null) {
      (media.parent as? ViewGroup)?.removeView(media)
      mediaView.removeAllViews()
      mediaView.addView(media, FrameLayout.LayoutParams(
          ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.MATCH_PARENT))
      adView.mediaView = media
  }

  adView.bodyView = body
  adView.headlineView = title
  adView.ctaView = cta
  adView.logoView = logo
  adView.advertiserView = info
  adView.ratingBarView = ratingBar
  logo.visibility = View.VISIBLE
  // Load logo url using any Image loading library (Glide is just an example here)
  Glide.with(applicationContext).load(ad.logo).into(logo)

  // Set native ad elements with data
  title.text = ad.headLine
  body.text = ad.body
  title.visibility = View.VISIBLE
  body.visibility = View.VISIBLE
  info.visibility = View.VISIBLE
  cta.text = ad.callToAction
  info.text = ad.advertiser
  ad.starRating?.let { ratingBar.rating = it.toFloat() }

  val map = HashMap<String, View>()
  map["headline"] = title
  map["body"] = body
  map["cta"] = cta
  map["advertiser"] = info

  // Send views to AdSter sdk for tracking click/impressionn etc.
  ad.trackViews(adView, null, map)
  // Set MediationNativeAd object
  adView.nativeAd = ad
  // Ad native ad view to container
  container.removeAllViews()
  container.addView(adView)
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Make sure to call `trackViews` and `setNativeAd` method before adding `MediationNativeAdView` to the container.
{% endhint %}

If you inflate with `attachToRoot = false`, add the inflated child to `adView` before adding `adView` to the screen container. Keep the SDK media view inside this native ad layout.

6. Call `MediationNativeAd.destroy` when activity or fragment is getting destroyed.

### Media sizing

Use a bounded media container, as in the 160dp-high example above, and add the SDK media view with `MATCH_PARENT` width and height. For a dynamic layout, set the container's layout parameters for its parent and follow the same binding sequence: register asset views, call `trackViews`, set `nativeAd`, then attach the ad view. Video preserves its aspect ratio and may have empty space around it.

## Native video playback

These playback controls apply to AdSter-served native video. Keep the SDK-provided `mediaView` in your layout so the SDK can handle playback, controls, and video tracking. Image ads and other networks may return a null `videoController`; always check it. For AdSter custom native video, use `mediaView`, even when `getMediaContent()` is null. Google media content follows the separate GAM path.

The SDK begins preparing video after loading the creative. Playback starts automatically when the media view is attached, has window focus, is shown, has a visible on-screen area, and its rendering surface is ready. It starts muted by default. Keep hardware acceleration enabled for the video view; playback failure falls back to the poster image.

### Start with sound

To start unmuted, call `unmute()` on the main thread in `onNativeAdLoaded`, before your display method attaches the ad view. This also works before the player finishes preparing. Apply the choice to every newly loaded ad; each starts with the muted default.

{% tabs %}
{% tab title="Java" %}
```java
// Inside onNativeAdLoaded(MediationNativeAd ad), before displaying it:
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
// Inside onNativeAdLoaded(ad: MediationNativeAd), before displaying it:
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
// When permanently removing the ad (ad is the retained MediationNativeAd):
ad.destroy();
// Remove its view from your container and clear your retained ad reference.
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
// When permanently removing the ad (ad is the retained MediationNativeAd):
ad.destroy()
// Remove its view from your container and clear your retained ad reference.
```
{% endtab %}
{% endtabs %}
