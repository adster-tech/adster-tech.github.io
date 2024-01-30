# 💡 Initialising the SDK



{% tabs %}
{% tab title="Java" %}
```java
AdSter.INSTANCE.initializeSdk(getApplicationContext(), AdapterStatus -> {
    // Initialization completes here
})
```
{% endtab %}

{% tab title="Kotlin" %}
```java
AdSter.initializeSdk(getApplicationContext(), object : InitializationListener {
    override fun onInitializationComplete(adapterStatus: List<AdapterStatus>) {
        // Initialization completes here
    }
})
```
{% endtab %}
{% endtabs %}
