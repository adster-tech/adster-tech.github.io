---
description: Below are the steps to load and show a custom native ad on your app
---

# 📪 Custom Native Ad

1. Create your `AdRequestConfiguration` as per the below format

```java
val configuration = AdRequestConfiguration(context,"Your_placement_name")
```

2. Call `loadAd()` method as per below format

{% tabs %}
{% tab title="Java" %}
```java
AdSter.INSTANCE.loadAd(configuration, new AdsEventListener() {
  @Override
    public void onNativeCustomFormatAdLoaded(@NonNull MediationNativeCustomFormatAd ad) {
      super.onNativeCustomFormatAdLoaded(ad);
    }

  @Override
    public void onFailure(@NonNull AdError adError) {
      // Handle Failure here
    }
});
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
AdSter.loadAd(configuration, object : AdsEventListener() {
  override fun onNativeCustomFormatAdLoaded (ad: MediationNativeCustomFormatAd) {
    super. onNativeCustomFormatAdLoaded (ad)
    // Show Reward ad here
  }
  override fun onFailure(adError: AdError) {
    // Handle failure here
  }
})
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
    
    <FrameLayout
        android:id="@+id/mediaView"
        android:layout_width="54dp"
        android:layout_height="54dp"
        android:visibility="gone"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        app:layout_constraintBottom_toBottomOf="parent"
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
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent" />

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

  ad.getDisplayOpenMeasurement();
  ad.recordImpression();

  adView.setBodyView(body);
  adView.setHeadlineView(title);
  adView.setCtaView(cta);
  adView.setLogoView(logo);
  adView.setAdvertiserView(info);

  logo.setVisibility(View.VISIBLE);
  Glide.with(getApplicationContext()).load(ad.getImage("Image").getDrawable()).into(logo);

  title.setText(ad.getText("Headline"));
  body.setText(ad.getText("Body"));
  cta.setText(ad.getText("Calltoaction"));
  info.setText(ad.getText("Attribution"));

  cta.setOnClickListener(new View.OnClickListener() {
    @Override
      public void onClick(View v) {
        ad.performClick((String) Objects.requireNonNull(ad.getText("clickactionURL")));
      }
  });

  Map<String, View> map = new HashMap<>();
  map.put("headline", title);
  map.put("body", body);
  map.put("cta", cta);
  map.put("advertiser",info);
  bannerScroll.addView(nativeAdView);
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

  ad.displayOpenMeasurement
  ad.recordImpression()

  adView.bodyView = body
  adView.headlineView = title
  adView.ctaView = cta
  adView.logoView = logo
  adView.advertiserView = info

  logo.visibility = View.VISIBLE
  Glide.with(applicationContext).load(ad.getImage("Image").getDrawable()).into(logo)

  title.text = ad.getText("Headline")
  body.text = ad.getText("Body")
  cta.text = ad.getText("Calltoaction")
  info.text = ad.getText("Attribution")

  cta.setOnClickListener {
    ad.performClick(ad.getText("clickactionURL").toString())
  }

  val map: MutableMap<String, View> = HashMap()
  map["headline"] = title
  map["body"] = body
  map["cta"] = cta
  map["advertiser"] = info
  bannerScroll.addView(nativeAdView)
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Make sure to call `trackViews` and `setAdvertiserView` method before adding `MediationNativeCustomFormatAd` to the container.
{% endhint %}

6. Call `MediationNativeCustomFormatAd.destroy` when activity or fragment is getting destroyed.
