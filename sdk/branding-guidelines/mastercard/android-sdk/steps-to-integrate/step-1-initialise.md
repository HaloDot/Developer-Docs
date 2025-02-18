# Step 1: Initialise

Mastercard Sonic Branding - Android SDK provides `SonicController` and `SonicView` as a public interface to the sdk.

#### Sonic Controller <a href="#sonic-controller" id="sonic-controller"></a>

`SonicController` provides a set of APIs for playing sound, animation, and haptics feedback. Initialize `SonicController` as follows:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
import androidx.fragment.app.Fragment
import com.mastercard.sonic.controller.SonicController

class SonicFragment : Fragment(R.layout.fragment_sonic) {

    private val sonicController = SonicController()
    
}

```
{% endtab %}

{% tab title="Java" %}
```java
import androidx.fragment.app.Fragment;
import com.mastercard.sonic.controller.SonicController;

public class SonicFragment extends Fragment {

    private SonicController sonicController = new SonicController();

    public SonicFragment(){

    }
}
```
{% endtab %}
{% endtabs %}

`SonicController` exposes the following methods:

| Method                                                                                                                                                                                                                                                           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| <p>fun prepare(sonicType: SonicType = SonicType.SOUND_AND_ANIMATION,<br>sonicCue: String,<br>sonicEnvironment: SonicEnvironment,<br>merchant: SonicMerchant,<br>isHapticsEnabled: Bool = true,<br>context: Context,<br>onPrepareListener: OnPrepareListener)</p> | <p><code>prepare()</code> method to prepare a set of resources with below parameters<br><code>sonicType</code> param for sonic type merchant app wants to prepare<br><code>sonicCue</code> param for the cue merchant app wants to prepare<br><code>sonicEnvironment</code> Environment for which sonic is getting prepared<br>production - for production environment<br>sandbox - for development and testing.<br><code>merchant</code> merchant information for that sonic is getting prepared<br><code>isHapticsEnabled</code> enabling/disabling haptics feedback, default value is true.<br><code>context</code> is current state of the application<br><code>OnPrepareListener.onPrepared</code> callback with status code as success, partial success, or failure.</p> |
| fun play(sonicView: SonicView? = null, onCompleteListener: OnCompleteListener)                                                                                                                                                                                   | <p><code>play()</code> should be call after successful <code>prepare()</code>. This plays the sonic (sound and/or animation)<br><code>sonicView</code> the view in which animation will play<br><code>completion</code> provides status in callback with status code success, partially success or fail.</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |

\


#### Sonic View <a href="#sonic-view" id="sonic-view"></a>

`SonicView` is a custom view that displays the Sonic Animation with a background. You can add `SonicView` into the parent view with any width and height value. It is recommended to provide the following properties to `SonicView` with a proper value.

| Property               | Description                                                                       | Type    | Default Value                                    |
| ---------------------- | --------------------------------------------------------------------------------- | ------- | ------------------------------------------------ |
| android:layout\_width  | Set the width                                                                     | Integer | `320dp`, if width is provided as `wrap_content`  |
| android:layout\_height | Set the height                                                                    | Integer | `240dp`, if height is provided as `wrap_content` |
| sonicBackground        | Set the sonic background color. It can set background color as `black` or `white` | Enum    | `black`                                          |

{% hint style="info" %}
Note: It is recommended to add `SonicView` on a full screen without padding. Padding is used to add space between two views. When you add padding to the `SonicView`, the background of the parent view gets displayed in the padded part which can lead to a bad user experience.
{% endhint %}

You can add `SonicView` either in XML or programmatically as follows:

* **Add `SonicView` in XML**

{% tabs %}
{% tab title="Xml" %}
```xml
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <!-- SonicView in a full screen -->
    <com.mastercard.sonic.widget.SonicView
        android:id="@+id/sonic_view"
        android:layout_width="0dp"
        android:layout_height="0dp"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
        <!-- app:sonicBackground="white" will enable white background when animation will be played-->
        <!-- app:sonicBackground="black" will enable black background when animation will be played-->
</androidx.constraintlayout.widget.ConstraintLayout>

```
{% endtab %}
{% endtabs %}

Create an instance of `SonicView` in Fragment/Activity.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
// import SonicView
import com.mastercard.sonic.widget.SonicView

// Create SonicView instance 
private lateinit var sonicView: SonicView

    override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): View? {
            return inflater.inflate(R.layout.fragment_sonic, container, false)
    }

    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
           super.onViewCreated(view, savedInstanceState)
           sonicView = view.findViewById(R.id.sonic_view)
           sonicView.background = SonicBackground.BLACK
    }

```
{% endtab %}

{% tab title="Java" %}
```java
// import SonicView
import com.mastercard.sonic.widget.SonicView;
// Create SonicView instance
private SonicView sonicView;

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
         return inflater.inflate(R.layout.fragment_sonic, container, false);
    }

    @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        sonicView = view.findViewById(R.id.sonic_view);
        sonicView.background = SonicBackground.BLACK;
    }


```
{% endtab %}
{% endtabs %}

* **Add `SonicView` Programmatically**

Create a blank layout file in the project and add the following:

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:id="@+id/main_content">

</androidx.constraintlayout.widget.ConstraintLayout>
```

Add `SonicView` as a child to `ConstraintLayout`.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
//import statement
import android.os.Bundle
import android.view.View
import androidx.constraintlayout.widget.ConstraintLayout
import com.mastercard.sonic.widget.SonicView

    //declare sonic view in a fragment
    private lateinit var sonicView: SonicView
    
    //declare onCreateView with a newly created layout file
    override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): View? {
                return inflater.inflate(R.layout.fragment_sonic, container, false)
        }

    //create sonicView instance and add to parent view in onViewCreated method
    override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
        super.onViewCreated(view, savedInstanceState)
        var constraintLayout : ConstraintLayout = view.findViewById(R.id.main_content)
        sonicView = SonicView(requireContext())
        constraintLayout.addView(sonicView)
        sonicView.layoutParams = ConstraintLayout.LayoutParams(ConstraintLayout.LayoutParams.MATCH_PARENT, ConstraintLayout.LayoutParams.MATCH_PARENT)
    }

```
{% endtab %}

{% tab title="Java" %}
```java
//import statement
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.constraintlayout.widget.ConstraintLayout;
import com.mastercard.sonic.widget.SonicView;

    //declare sonicView in a fragment
    private SonicView sonicView;

    //declare onCreateView with a newly created layout file
    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
         return inflater.inflate(R.layout.fragment_sonic, container, false);
    }

    //create sonicView and add it to parent view in onViewCreated 
    @Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        ConstraintLayout constraintLayout = view.findViewById(R.id.main_content);
        sonicView = new SonicView(getContext());
        sonicView.setLayoutParams(new ConstraintLayout.LayoutParams(ConstraintLayout.LayoutParams.MATCH_PARENT, ConstraintLayout.LayoutParams.MATCH_PARENT));
        constraintLayout.addView(sonicView);
    }

```
{% endtab %}

{% tab title="ComposeUI" %}
```ruby
@Composable
fun SonicViewComposable(onViewCreated: (SonicView) -> Unit) {
    val context = LocalContext.current
    val sonicView = remember { SonicView(context) }
    AndroidView(factory = { sonicView.also { it.background = SonicBackground.BLACK } },
        modifier = Modifier.fillMaxWidth().fillMaxHeight()) { view ->
        onViewCreated(view)
    }
}

```
{% endtab %}
{% endtabs %}

#### Sonic Merchant <a href="#sonic-merchant" id="sonic-merchant"></a>

`SonicMerchant` needs to be initialized and required to be pass it in `prepare()` method.

{% tabs %}
{% tab title="Kotlin" %}
```javascript
    private lateinit var sonicMerchant: SonicMerchant

    sonicMerchant = SonicMerchant.Builder()
                .merchantName("Uber")
                .city("New York")
                .merchantCategoryCodes(arrayOf("MCC 5122"))
                .countryCode("USA")
                .merchantId("UberId")
                .build()

```
{% endtab %}

{% tab title="Java" %}
```java
    private SonicMerchant sonicMerchant;
    
    sonicMerchant = new SonicMerchant.Builder()
            .merchantName("Uber")
            .city("New York")
            .merchantCategoryCodes(new String[]{"MCC 5122"})
            .countryCode("USA")
            .merchantId("UberId")
            .build();

```
{% endtab %}
{% endtabs %}

Below properties needs to be provided by merchant to configure `SonicMerchant`.

<table data-full-width="true"><thead><tr><th width="200">Property</th><th>Description</th><th width="157">Type</th><th>Required</th><th>Reference</th></tr></thead><tbody><tr><td><code>merchantName</code></td><td>Name that the business is known by. It will be the name that is used on all official communications. This information can be obtained by contacting your payment processor, acquiring bank’s customer support and merchant services department or Mastercard Representative.<br>Note: If you are a service provider that engages in 1-to-many integrations, you can include your business name</td><td>String</td><td>Yes</td><td></td></tr><tr><td><code>merchantId</code></td><td>Merchant ID (Merchant Identification Number) is a unique identifier(15-digit code) assigned to each merchant at a time of onboarding process by their payment processor or acquiring bank for Mastercard Transactions.<br>This information can be obtained by contacting payment processor or acquiring bank’s customer support or merchant services department.</td><td>String</td><td>No</td><td></td></tr><tr><td><code>countryCode</code></td><td>3 digit ISO country code of the merchant accepting the Mastercard payments. The country is identified based on the country where the POS device is installed and accepting payments, or the merchant’s country associated with its app.</td><td>String</td><td>Yes</td><td>‘USA’<br><a href="https://developer.mastercard.com/mastercard-sonic-branding/documentation/android/code-and-formats/#country-codes">Country Codes</a></td></tr><tr><td><code>city</code></td><td>City of the merchant is identified based on the location where the POS device is installed and accepting Mastercard payments, or the merchant’s city associated with its app.</td><td>String</td><td>No</td><td></td></tr><tr><td><code>merchantCategoryCodes</code></td><td>Merchant Category Code (MCC) is a four-digit code used to categorize businesses based on the type of products or services. This information can be obtained by contacting your payment processor, acquiring bank’s customer support and merchant services department or Mastercard Representative.<br>Note: If you are a service provider that engages in 1-to-many integrations, please insert [‘MCC 0000’]</td><td>String[]</td><td>Yes</td><td>[‘MCC 5122’]<br><a href="https://www.mastercard.us/content/dam/mccom/en-us/documents/rules/quick-reference-booklet-merchant-edition.pdf">Codesopens in a new tab</a></td></tr></tbody></table>
