# 📪 Rewarded Ad

{% tabs %}
{% tab title="Java" %}
```java
AdSter.INSTANCE.setRewardedAdListener(new RewardedAdEventsCallback() {
  @Override
    public void onUserEarnedReward(@NonNull Reward reward) {
      // Called when the user is eligible for a reward
    }

  @Override
    public void onAdClicked() {
      // Called when ad is clicked
    }

  @Override
    public void onAdImpression() {
      // Called when ad is getting impression
    }

  @Override
    public void onVideoComplete() {
      // Called when rewarded video completed
    }

  @Override
    public void onVideoStart() {
      // Called when the rewarded video started.
    }
});
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
AdSter.setRewardedAdListener(object : RewardedAdEventsCallback() {
  override fun onUserEarnedReward(@NonNull reward: Reward) {
    // Called when user is eligible for a reward
  }
  override fun onAdClicked() {
    // Called when ad is clicked
  }
  override fun onAdImpression() {
    // Called when ad is getting impression
  }
  override fun onVideoComplete() {
    // Called when rewarded video completed
  }
  override fun onVideoStart() {
    // Called when rewarded video started.
  }
});
```
{% endtab %}
{% endtabs %}
