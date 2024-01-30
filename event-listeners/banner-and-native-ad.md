# 📪 Banner and Native Ad

{% tabs %}
{% tab title="Java" %}
```java
AdSter.INSTANCE.setAdListener(new AdEventsCallback() {
  @Override
    public void onAdImpression() {
      // Called when Ad is getting impressions
    }

  @Override
    public void onAdClicked() {
      // Called when Ad is clicked
    }
});
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
AdSter.setAdListener(object : AdEventsCallback() {
  override fun onAdImpression() {
    // Called when Ad is getting impressions
  }
  override fun onAdClicked() {
    // Called when Ad is clicked
  }
});
```
{% endtab %}
{% endtabs %}
