# Step 3: Play

On successful preparation, call `play()` method to play Mastercard Sonic Feedback.

{% hint style="info" %}
Note:Mastercard Sonic Branding Sound and/or Animation play process is divided into two steps as mentioned below:\
1\). `prepare()`

2\). `play()`\
`sonicController.play` must be followed by `sonicController.prepare` call.
{% endhint %}



{% tabs %}
{% tab title="Kotlin" %}
```kotlin
//import statements
import android.util.Log
import com.mastercard.sonic.listeners.OnCompleteListener

//Create private fun to play sonic
    private fun playSonic() {
        sonicController.play(
        sonicView,
        object : OnCompleteListener {
            override fun onComplete(statusCode: Int) {
                Log.d("SonicFragment", "SonicView is played successfully, statusCode=$statusCode")
            }
        })
    }

```
{% endtab %}

{% tab title="Java" %}
```java
//import statements
import android.util.Log;
import com.mastercard.sonic.listeners.OnCompleteListener;

//Add playSonic Method 
    private void playSonic() {
        sonicController.play(
            sonicView,
            new OnCompleteListener() {
            @Override
            public void onComplete(int statusCode) {
                Log.d("SonicFragment", "SonicView is played successfully, statusCode=$statusCode");
            }
        });        
    }

```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Note: In case of sound only, `SonicView` can be passed as null.
{% endhint %}

For complete list of StatusCode, click [here](https://developer.mastercard.com/mastercard-sonic-branding/documentation/android/code-and-formats/#status-code).
