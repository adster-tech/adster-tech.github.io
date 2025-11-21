---
description: >-
  To Initialize the SDK call the intitializeSDK() function in the application
  class of the app. It is recommended to call the function as soon as possible.
---

# 💡 Initializing the SDK

The initializeSDK() function returns a list of AdapterStatus , and the function is called as follows:

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

Note : All load ad requests are to be called only after the completion of the initialization of the SDK.
