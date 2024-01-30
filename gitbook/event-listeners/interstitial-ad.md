# 📪 Interstitial Ad

{% tabs %}
{% tab title="Java" %}
```java
AdSter.INSTANCE.setInterstitialAdListener(new InterstitialAdEventsCallback() {
  @Override
    public void onAdClicked() {
      // Called when Ad is clicked
    }

  @Override
    public void onAdImpression() {
      // Called when Ad is getting impressions
    }

  @Override
    public void onAdOpened() {
      // Called when Ad is opened
    }

  @Override
    public void onAdClosed() {
      // Called when Ad is closed
    }
});
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
AdSter.setInterstitialAdListener(object : InterstitialAdEventsCallback() {
  override fun onAdClicked() {
    // Called when Ad is clicked
  }
  override fun onAdImpression() {
    // Called when Ad is getting impressions
  }
  override fun onAdOpened() {
    // Called when Ad is opened
  }
  override fun onAdClosed() {
    // Called when Ad is closed
  }
});
```
{% endtab %}
{% endtabs %}
