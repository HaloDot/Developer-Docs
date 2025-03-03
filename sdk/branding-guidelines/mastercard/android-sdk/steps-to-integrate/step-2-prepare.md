# Step 2: Prepare

After the initialization is completed, select below parameters to prepare and play sonic feedback

Select one of the following `sonicType`.

> * `SOUND_AND_ANIMATION (default)`
> * `SOUND_ONLY`
> * `ANIMATION_ONLY`

Select one of the following `SonicEnvironment`.

> * `SANDBOX`
> * `PRODUCTION`

`PRODUCTION` is used for production environment else select `SANDBOX` for development and testing.

Select one of the following `sonicCue`.

> * `checkout`
> * `securedby`

Enable/disable haptic feedback `isHapticsEnabled`.

> * `true (default)`
> * `false`

* **Sound and Animation**

Invoke `prepare()` method of `SonicController` providing `SonicType` as `SonicType.SOUND_AND_ANIMATION` , `SonicEnvironment` as `SANDBOX` and `sonicCue` as `checkout`. This method loads the sound, animation, and haptic resources. On preparation, it returns `StatusCode.SUCCESS` in `onPrepared()` as a part of `OnPrepareListener()`. On successful preparation, call `play()` method to play Mastercard Sonic Sound and Animation.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
//import statements
import android.util.Log
import com.mastercard.sonic.controller.SonicType
import com.mastercard.sonic.listeners.OnPrepareListener

//invoke prepare call in onViewCreated method
sonicController.prepare(
            sonicType = SonicType.SOUND_AND_ANIMATION,
            sonicCue = sonicCue,
            sonicEnvironment = SonicEnvironment.SANDBOX,
            merchant = sonicMerchant,
            isHapticsEnabled = true,
            context = requireContext().applicationContext,
            onPrepareListener = object :
                OnPrepareListener {
                override fun onPrepared(statusCode: Int) {
                    Log.d("SonicFragment", "SonicView is prepared, statusCode=$statusCode")
                    playSonic() // Refer to Step 3: Play
                }
            })


```
{% endtab %}

{% tab title="Java" %}
```java
//import statements
import android.util.Log;
import com.mastercard.sonic.controller.SonicType;
import com.mastercard.sonic.listeners.OnPrepareListener;

//add prepare call in onViewCreated method
@Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        sonicController.prepare(SonicType.SOUND_AND_ANIMATION, sonicCue, SonicEnvironment.SANDBOX, sonicMerchant, requireContext().getApplicationContext(), new OnPrepareListener(){
            @Override
            public void onPrepared(int statusCode) {
                Log.d("SonicFragment", "SonicView is prepared, statusCode="+ statusCode);
                playSonic(); // Refer to Step 3: Play
            }
        });
    }

 world"
print(message)
```
{% endtab %}
{% endtabs %}



* **Sound Only**

Invoke `prepare()` method of `SonicController` providing `SonicType` as `SonicType.SOUND_ONLY` , `SonicEnvironment` as `SANDBOX` and `sonicCue` as `checkout`. This method loads the sound resource only. On preparation, it returns `StatusCode.SUCCESS` in `onPrepared()` as a part of `OnPrepareListener()`.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
//import statements
import android.util.Log
import com.mastercard.sonic.controller.SonicType
import com.mastercard.sonic.listeners.OnPrepareListener

//Add prepare call in onViewCreated method
sonicController.prepare(
            sonicType = SonicType.SOUND_ONLY,
            sonicCue = sonicCue,
            sonicEnvironment = SonicEnvironment.SANDBOX,
            merchant = sonicMerchant,
            isHapticsEnabled = true,
            context = requireContext().applicationContext,
            onPrepareListener = object :
                OnPrepareListener {
                override fun onPrepared(statusCode: Int) {
                    Log.d("SonicFragment", "Sound prepared, statusCode=$statusCode")
                    playSonic() // Refer to Step 3: Play
                }
            })


```
{% endtab %}

{% tab title="Java" %}
```java
//import statements
import android.util.Log;
import com.mastercard.sonic.controller.SonicType;
import com.mastercard.sonic.listeners.OnPrepareListener;

//add prepare call in onViewCreated method
@Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        sonicController.prepare(SonicType.SOUND_ONLY, sonicCue, SonicEnvironment.SANDBOX, sonicMerchant, getContext()requireContext().getApplicationContext(), new OnPrepareListener(){
            @Override
            public void onPrepared(int statusCode) {
                Log.d("SonicFragment", "Sound prepared, statusCode="+ statusCode);
                playSonic(); // Refer to Step 3: Play
            }
        });
    }

```
{% endtab %}
{% endtabs %}

* **Animation Only**

Invoke `prepare()` method of `SonicController` providing `SonicType` as `SonicType.ANIMATION_ONLY` , `SonicEnvironment` as `SANDBOX` and `sonicCue` as `securedby`. This method loads the animation resource. On preparation, it returns the `StatusCode.SUCCESS` in `onPrepared()` as part of `OnPrepareListener()`. On successful preparation, call `play()` method to play Mastercard Checkout Animation.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
//import statements
import android.util.Log
import com.mastercard.sonic.controller.SonicType
import com.mastercard.sonic.listeners.OnPrepareListener

//Add prepare call in onViewCreated method
sonicController.prepare(
            sonicType = SonicType.ANIMATION_ONLY,
            sonicCue = sonicCue,
            sonicEnvironment = SonicEnvironment.SANDBOX,
            merchant = sonicMerchant,
            isHapticsEnabled = true,
            context = requireContext().applicationContext,
            onPrepareListener = object :
                OnPrepareListener {
                override fun onPrepared(statusCode: Int) {
                    Log.d("SonicFragment", "SonicView is prepared, statusCode=$statusCode")
                    playSonic() // Refer to Step 3: Play
                }
            })

```
{% endtab %}

{% tab title="Java" %}
```java
//import statements
import android.util.Log;
import com.mastercard.sonic.controller.SonicType;
import com.mastercard.sonic.listeners.OnPrepareListener;

//add prepare call in onViewCreated method
@Override
    public void onViewCreated(@NonNull View view, @Nullable Bundle savedInstanceState) {
        super.onViewCreated(view, savedInstanceState);
        sonicController.prepare(SonicType.ANIMATION_ONLY, sonicCue, SonicEnvironment.SANDBOX, sonicMerchant, getContext()requireContext().getApplicationContext(), new OnPrepareListener(){
            @Override
            public void onPrepared(int statusCode) {
                Log.d("SonicFragment", "SonicView is prepared, statusCode="+ statusCode);
                playSonic(); // Refer to Step 3: Play
            }
        });
    }

```
{% endtab %}
{% endtabs %}

* **Haptics Feedback**

This feature is enabled through our public facing method prepare(), which excepts a boolean parameter `isHapticsEnabled`, by default this parameter is set to true. Currently, haptics is only supported on the “checkout” Sonic cue.

Troubleshooting Haptics Feedback

There are two scenarios in which haptics preparation may fail:

1. Device Compatability: Haptics feedback will fail to play if the device does not support haptics. The minimum Android version supporting haptics functionality is Android 8 (API level 26)) and above.
2. Unsupported Sonic Cue: Attempting to prepare haptics on a cue that does not support haptics will result in preparation failure.

\
