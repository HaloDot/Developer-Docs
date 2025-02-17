# Step 2: Integration

## a. Import the SDK Module

1\. Copy the ${sdkFolder}/visa-sensory-branding-sdk module to your project, it's a pre-configured Gradle module for visa-sensory-branding-${sdkVersion}.aar.&#x20;

2\. Add the SDK module to your own modules' build.gradle(.kts) by the below code:&#x20;

```kotlin
dependencies { 
... implementation(project(":visa-sensory-branding-sdk")) 
}
```

3\. Click Gradle Sync button of Android Studio to load the SDK.&#x20;

4\. You can find the integration examples under folders inside the package.&#x20;

## b. Initialisation

Import the Visa Sensory Branding class reference into source files as necessary.

{% tabs %}
{% tab title="Java/Kotlin" %}
```java
import com.visa.SensoryBrandingView
```
{% endtab %}

{% tab title="XML" %}
```xml
<com.visa.SensoryBrandingView
android:id="@+id/vsb"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:layout_centerInParent="true"/>
```
{% endtab %}

{% tab title="Java + View" %}
```java
SensoryBrandingView vsb = (SensoryBrandingView) findViewById(R.id.vsb);
```
{% endtab %}

{% tab title="Kotlin + View" %}
```kotlin
val vsb = findViewById<SensoryBrandingView>(R.id.vsb)
```


{% endtab %}

{% tab title="Kotlin + Jetpack Compose" %}
```kotlin
// Wrap the SensoryBrandingView with AndroidView
AndroidView( modifier = Modifier
.width(Dp(width))
.wrapContentHeight(),
factory = { ctx ->
val vsb = SensoryBrandingView(ctx, null)
// More configurations...
// vsb.languageCode = "en"
vsb
},
update = { vsb -> })
```
{% endtab %}
{% endtabs %}

## c. Animate

Activates the Visa Sensory Branding animation.

{% tabs %}
{% tab title="Java + View" %}
```java
vsb.animate(error -> {
Log.d("SensoryBrandingView", error == null ? "OK" : error.getMessage());
return null;
});
```
{% endtab %}

{% tab title="Kotlin + View" %}
```kotlin
vsb.animate { error ->
Log.d("SensoryBrandingView", error?.message ?: "OK")
}
```
{% endtab %}

{% tab title="Kotlin + Jetpack Compose" %}
```kotlin
// We need a property to trigger animation
var playingTheAnimation by rememberSaveable { mutableStateOf(false) }

// Wrap the SensoryBrandingView with AndroidView
AndroidView(
modifier = Modifier
.width(Dp(width))
.wrapContentHeight(),
factory = { ctx ->
val vsb = SensoryBrandingView(ctx, null)
// More configurations...
// vsb.languageCode = "en"
vsb
},
update = { vsb ->
if (playingTheAnimation) {
vsb.animate { result ->
Log.d("SensoryBrandingView", result?.message ?: "OK")
}
}
})
```
{% endtab %}
{% endtabs %}

There are 3 possible error messages (Error#getMessage()):

| Error Message                                                                            | NOTE                                            |
| ---------------------------------------------------------------------------------------- | ----------------------------------------------- |
| Previous animation still in progress, cannot start new animation                         | Please wait for a while till animation displays |
| Alpha channel is not supported for backdrop color                                        | Please choose a different background color      |
| Invalid background color selected, contrast levels are below 3:1 against #FFFFFF #1434CB | Please choose a different background color      |

## d. Sizing & Layout

You can choose to have the Visa animation render in full screen on a device, or in a constrained view in context of other UI elements. To render in full screen, simply initialize the container to fit device height and width and set background color to same as backdropColor. For constrained view, specify the width of SensoryBrandingView during initialization.&#x20;

1. The width of the animation object will not be larger than 60% of the screen's width. If the width is set to be larger, it will be resized to be 60% of the screen's width.&#x20;
2. &#x20;The width of the animation object will not be smaller than 20% of the screen's width. If the width is set to be smaller, it will be resized to be 20% of the screen's width.&#x20;

## e. Animation Configuration Parameters

**Language Code**

Define the language of the texts present below the checkmark

{% tabs %}
{% tab title="Java" %}
```java
vsb.setLanguageCode("en");
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
vsb.languageCode = "en"
```
{% endtab %}
{% endtabs %}

**Backdrop Color**

The color behind the animation, used to determine the Visa logo colors. Specify Visa Blue(#1434CB) for a white Visa logo. Specify White(#FFFFFF) for a blue Visa logo. Any other color will result in either blue or white color applied to the Logo, depending on contrast.&#x20;

Note: Do not set backdropColor with simi-transparent color or make it transparent.

{% tabs %}
{% tab title="Java" %}
```java
vsb.setBackdropColor(Color.parseColor("#123333"));
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
vsb.backdropColor = Color.parseColor("#123333")
```
{% endtab %}
{% endtabs %}

**Sound**

Set to true to enable sound. (true by default)

{% tabs %}
{% tab title="Java" %}
```java
vsb.setSoundEnabled(true);
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
vsb.soundEnabled = true
```
{% endtab %}
{% endtabs %}

**Checkmark**

This parameter enables/disables checkmark screen after visa logo animation:&#x20;

Checkmark Mode includes:&#x20;

* CheckmarkMode.CHECKMARK: shows checkmark at the end of the animation without text&#x20;
* CheckmarkMode.CHECKMARK\_WITH\_TEXT: shows checkmark and checkmark text at the end of the animation (default)&#x20;
* CheckmarkMode.NONE: no checkmark at the end of the animation&#x20;

Checkmark Text includes:&#x20;

* CheckmarkTextOption.APPROVE&#x20;
* CheckmarkTextOption.SUCCESS&#x20;
* CheckmarkTextOption.COMPLETE (default)&#x20;

{% tabs %}
{% tab title="Java" %}
```java
vsb.setCheckmarkMode(CheckmarkMode.CHECKMARK_WITH_TEXT);
vsb.setCheckmarkText(CheckmarkTextOption.APPROVE);
```
{% endtab %}

{% tab title="Kotlin" %}
```kotlin
vsb.checkmarkMode = CheckmarkMode.CHECKMARK_WITH_TEXT
vsb.checkmarkText = CheckmarkTextOption.APPROVE
```
{% endtab %}
{% endtabs %}





