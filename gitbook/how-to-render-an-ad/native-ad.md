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
    public void onAdRevenuePaid(double revenue, @NotNull String adUnitId,@NotNull String network) {
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
    
    override fun onAdRevenuePaid(revenue: Double, adUnitId: String, network: String) {
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

  // If MediaView is present add AdSter's MediaView as a child to given MediaView
  if (ad.getMediaView() != null) {
      mediaView.addView(ad.getMediaView());
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
  val ratingBar : RaringBar = adView.findViewById(R.id.ratingBar)
  // MediaView
  val mediaView: FrameLayout = nativeAdView.findViewById(R.id.mediaView)

  // If MediaView is present add AdSter's MediaView as a child to given MediaView
  if (ad.mediaView != null) {
      mediaView.addView(ad.mediaView)
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
  cta.text = ad.callToAction
  info.text = ad.advertiser
  starRating?.let { ratingBar.rating = it.toFloat() }

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

{% hint style="info" %}
```
If you set attachToRoot as false for further customization of nativeAdView before displaying, make sure you attach it to parent afterwards.
In the example provided above it is already set to true.
```
{% endhint %}

{% tabs %}
{% tab title="Java" %}
```javascript
View nativeAdView = LayoutInflater.from(this).inflate(R.layout.ad_native_layout, adView, false);
parent.addView(nativeAdView); 
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
val nativeAdView: View = LayoutInflater.from(this).inflate(R.layout.ad_native_layout, adView, true)
parent.addView(nativeAdView) 
```
{% endtab %}
{% endtabs %}

6. Call `MediationNativeAd.destroy` when activity or fragment is getting destroyed.

***

### Native Ad in Dynamic Layout

{% tabs %}
{% tab title="Java" %}
```java
AdSterAdLoader.Builder builder = new AdSterAdLoader.Builder()
        .withAdsListener(new MediationAdListener() {
            @Override
            public void onNativeAdLoaded(MediationNativeAd ad) {
                super.onNativeAdLoaded(ad);

                // Instantiating the dynamicMediaView Object
                FrameLayout dynamicMediaView = new FrameLayout(YourActivity.this);

                // Set the Width and Height based on your requirement
                dynamicMediaView.setLayoutParams(new LinearLayout.LayoutParams(800, 600));

                if (ad.getMediaView() != null) {
                    dynamicMediaView.addView(ad.getMediaView());
                    linearLayout.addView(dynamicMediaView);
                }
            }

            @Override
            public void onFailure(AdError adError) {
                // Handle failure callback here
            }
        })
        .withAdsEventsListener(new AdEventsListener() {
            @Override
            public void onAdClicked() {
                // Handle ad click here
            }

            @Override
            public void onAdImpression() {
                // Handle ad impression here
            }
        });

AdSterAdLoader adLoader = builder.build();
adLoader.loadAd(nativeConfiguration3.build());
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
AdSterAdLoader.builder().withAdsListener(object : MediationAdListener() {
    override fun onNativeAdLoaded(ad: MediationNativeAd) {
        super.onNativeAdLoaded(ad)
        //Instantiating the dynamicMediaView Object
        val dynamicMediaView = FrameLayout(this@YourActivity)
        //Set the Width and Height based on your requirement
        dynamicMediaView.layoutParams = LinearLayout.LayoutParams(800,600)
        if (ad.mediaView != null) {
            dynamicMediaView.addView(ad.mediaView)
            linearLayout.addView(dynamicMediaView)
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
}).build().loadAd(nativeConfiguration3.build())
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
{% code fullWidth="false" %}
```
Make sure you set LayoutParams of your dynamicMediaView in accordance to parent layout herein Linear Layout.
```
{% endcode %}
{% endhint %}

{% tabs %}
{% tab title="Java" %}
```javascript
dynamicMediaView.setLayoutParams(new LinearLayout.LayoutParams(800, 600));
```
{% endtab %}

{% tab title="Kotlin" %}
```python
dynamicMediaView.layoutParams = LinearLayout.LayoutParams(800,600)
```
{% endtab %}
{% endtabs %}
