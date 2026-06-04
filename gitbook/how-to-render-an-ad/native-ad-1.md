---
description: Below are the steps to load and show a native reward ad on your app
---

# 📪 Native Reward Ad

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

2. Adding PPID to AdRequest

```java
configuration.publisherProvidedId("YOUR_PPID");
```

3. Call `loadAd()` method as per below format

{% tabs %}
{% tab title="Java" %}
<pre class="language-java"><code class="lang-java">AdSterAdLoader.Companion.builder().withAdsListener(new MediationAdListener() {
    @Override
    public void onNativeRewardAdLoaded(@NonNull MediationNativeRewardAd ad) {
        super.onNativeRewardAdLoaded(ad);
<strong>        //Show native reward ad here
</strong>    }

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
</code></pre>
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
AdSterAdLoader.builder().withAdsListener(object : MediationAdListener() {    
    override fun onNativeRewardAdLoaded(ad: MediationNativeRewardAd) {
        super.onNativeRewardAdLoaded(ad)
        //Show native reward ad here
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

4. Inside the `onNativeRewardAdLoaded` callback method use `MediationNativeRewardAd` object to display native reward ad on your defined layout.
5. The layout below is only an example. The client app can design the reward UI independently.

{% code overflow="wrap" %}
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/nativeRewardLayout"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@android:color/white"
    android:padding="16dp">

    <LinearLayout
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:orientation="vertical"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent">

        <LinearLayout
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:gravity="center_vertical"
            android:orientation="horizontal">

            <ImageView
                android:id="@+id/iconLogoImageView"
                android:layout_width="48dp"
                android:layout_height="48dp"
                android:scaleType="centerCrop" />

            <LinearLayout
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_marginStart="12dp"
                android:layout_weight="1"
                android:orientation="vertical">

                <TextView
                    android:id="@+id/advertiserTextView"
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:ellipsize="end"
                    android:maxLines="1"
                    android:textColor="@android:color/black"
                    android:textSize="14sp"
                    tools:text="Advertiser" />

                <TextView
                    android:id="@+id/titleTextView"
                    android:layout_width="match_parent"
                    android:layout_height="wrap_content"
                    android:ellipsize="end"
                    android:maxLines="2"
                    android:textColor="@android:color/black"
                    android:textSize="18sp"
                    android:textStyle="bold"
                    tools:text="Native Reward Offer" />
            </LinearLayout>
        </LinearLayout>

        <FrameLayout
            android:id="@+id/mediaView"
            android:layout_width="match_parent"
            android:layout_height="180dp"
            android:layout_marginTop="16dp" />

        <TextView
            android:id="@+id/bodyTextView"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="12dp"
            android:ellipsize="end"
            android:maxLines="4"
            android:textColor="@android:color/black"
            android:textSize="14sp"
            tools:text="Complete the offer to receive the reward." />

        <Button
            android:id="@+id/ctaButton"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="16dp"
            tools:text="Redeem now" />
    </LinearLayout>
</androidx.constraintlayout.widget.ConstraintLayout>
```
{% endcode %}

6. The above sample layout can be used with the `MediationNativeRewardAd` object to render an ad as shown in the below example

{% tabs %}
{% tab title="Java" %}
```java
private MediationNativeRewardAd nativeRewardAd;

private void displayNativeRewardAd(MediationNativeRewardAd ad) {
    nativeRewardAd = ad;

    // Create AdSter MediationNativeRewardAdView object.
    MediationNativeRewardAd adView = new MediationNativeRewardAd(this);

    // Add this layout as a parent to your native reward ad layout.
    View nativeRewardAdView = LayoutInflater.from(this)
            .inflate(R.layout.native_reward_ad_layout, adView, true);

    TextView advertiser = adView.findViewById(R.id.advertiserTextView);
    TextView title = adView.findViewById(R.id.titleTextView);
    TextView body = adView.findViewById(R.id.bodyTextView);
    Button cta = adView.findViewById(R.id.ctaButton);
    ImageView logo = adView.findViewById(R.id.iconLogoImageView);
    FrameLayout mediaContainer = nativeRewardAdView.findViewById(R.id.mediaView);

    adView.setAdvertiserView(advertiser);
    adView.setHeadlineView(title);
    adView.setBodyView(body);
    adView.setCtaView(cta);
    adView.setLogoView(logo);

    advertiser.setText(ad.getAdvertiser());
    title.setText(ad.getHeadLine());
    body.setText(ad.getBody());
    cta.setText(ad.getCallToAction());

    if (ad.getLogo() != null) {
        // Load logo url using any image loading library. Glide is used only as an example.
        Glide.with(getApplicationContext()).load(ad.getLogo()).into(logo);
    }

    if (ad.getMediaView() != null) {
        View mediaView = ad.getMediaView();
        ViewParent parent = mediaView.getParent();
        if (parent instanceof ViewGroup) {
            ((ViewGroup) parent).removeView(mediaView);
        }
        mediaContainer.removeAllViews();
        mediaContainer.addView(mediaView);
        adView.setMediaView(mediaView);
    }

    Map<String, View> clickableViews = new HashMap<>();
    clickableViews.put("headline", title);
    clickableViews.put("body", body);
    clickableViews.put("cta", cta);
    clickableViews.put("advertiser", advertiser);

    // Send views to AdSter SDK for click and impression tracking.
    ad.trackViews(adView, logo, clickableViews);

    // Set MediationNativeRewardAd object.
    adView.setNativeRewardAd(ad);

    container.removeAllViews();
    container.addView(adView);

    if (ad.getHasReward()) {
        // Optional reward metadata. Client app owns how this reward is displayed or fulfilled.
        JsonObject reward = ad.getReward();
    }
}

@Override
protected void onDestroy() {
    if (nativeRewardAd != null) {
        nativeRewardAd.destroy();
        nativeRewardAd = null;
    }
    super.onDestroy();
}
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
private var nativeRewardAd: MediationNativeRewardAd? = null

private fun displayNativeRewardAd(ad: MediationNativeRewardAd) {
    nativeRewardAd = ad

    // Create AdSter MediationNativeRewardAdView object.
    val adView = MediationNativeRewardAdView(this)

    // Add this layout as a parent to your native reward ad layout.
    val nativeRewardAdView: View = LayoutInflater.from(this)
        .inflate(R.layout.native_reward_ad_layout, adView, true)

    val advertiser: TextView = adView.findViewById(R.id.advertiserTextView)
    val title: TextView = adView.findViewById(R.id.titleTextView)
    val body: TextView = adView.findViewById(R.id.bodyTextView)
    val cta: Button = adView.findViewById(R.id.ctaButton)
    val logo: ImageView = adView.findViewById(R.id.iconLogoImageView)
    val mediaContainer: FrameLayout = nativeRewardAdView.findViewById(R.id.mediaView)

    adView.advertiserView = advertiser
    adView.headlineView = title
    adView.bodyView = body
    adView.ctaView = cta
    adView.logoView = logo

    advertiser.text = ad.advertiser
    title.text = ad.headLine
    body.text = ad.body
    cta.text = ad.callToAction

    ad.logo?.let { logoUrl ->
        // Load logo url using any image loading library. Glide is used only as an example.
        Glide.with(applicationContext).load(logoUrl).into(logo)
    }

    ad.mediaView?.let { mediaView ->
        (mediaView.parent as? ViewGroup)?.removeView(mediaView)
        mediaContainer.removeAllViews()
        mediaContainer.addView(mediaView)
        adView.mediaView = mediaView
    }

    val clickableViews = hashMapOf<String, View>(
        "headline" to title,
        "body" to body,
        "cta" to cta,
        "advertiser" to advertiser
    )

    // Send views to AdSter SDK for click and impression tracking.
    ad.trackViews(adView, logo, clickableViews)

    // Set MediationNativeRewardAd object.
    adView.nativeRewardAd = ad

    container.removeAllViews()
    container.addView(adView)

    if (ad.hasReward) {
        // Optional reward metadata. Client app owns how this reward is displayed or fulfilled.
        val reward = ad.reward
    }
}

override fun onDestroy() {
    nativeRewardAd?.destroy()
    nativeRewardAd = null
    super.onDestroy()
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Make sure to call `trackViews` and set `NativeRewardAd` method before adding `MediationNativeRewardAdView` to the container.
{% endhint %}
