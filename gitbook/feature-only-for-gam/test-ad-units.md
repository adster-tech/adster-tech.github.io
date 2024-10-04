# TEST AD UNITS

Sample test adunits by Adster to ensure Ads are coming and is displayed inAPP by the developers.&#x20;



Adster\_Unified\_Test (can respond with either banner or native ads)

Adster\_Native\_Test (will respond with native ads only)

Adster\_Banner\_Test (will respond with banner ads only)

Adster\_Appopen\_Test (will respond with APPOpen ads only)

Adster\_Interstitial\_Test (will respond with Interstitial ads only)

Adster\_FS\_Native\_Test (will respond with native ads only for full screen opportunity, in case of swipe actions)&#x20;

Adster\_FS\_Unified\_Test (will respond with native or banner like 320x480 ads only for full screen opportunity, in case of swipe actions) )

E.g.&#x20;

val configuration = AdRequestConfiguration.Companion.builder(context, "Adster\_Banner\_Test");

