# Orientation-Changes  

To declare that your activity handles a configuration change, edit the appropriate `<activity>` element in your manifest file to include the `android:configChanges` attribute with a value that represents the configuration you want to handle.  
Possible values are listed in the documentation for the `android:configChanges` attribute.  

The most commonly used values are "orientation", "screenSize", "screenLayout", and "keyboardHidden":  

- The "orientation" value prevents restarts when the screen orientation changes.  
- The "screenSize" value also prevents restarts when orientation changes, but only for Android 3.2 (API level 13) and above.  
- The "screenLayout" value is necessary to detect changes that can be triggered by devices such as foldable phones and convertible Chromebooks.  
- The "keyboardHidden" value prevents restarts when the keyboard availability changes.  

If you want to manually handle orientation changes in your app you must declare the "orientation", "screenSize", and "screenLayout" values in the android:configChanges attributes.  
You can declare multiple configuration values in the attribute by separating them with a pipe | character.  

For example, the following manifest code declares an activity that handles both screen orientation changes and keyboard availability change:  
```xml
<activity android:name=".MyActivity"
          android:configChanges="orientation|screenSize|screenLayout|keyboardHidden"
          android:label="@string/app_name">
```
Now, when one of these configurations change, MyActivity does not restart. Instead, the MyActivity receives a call to `onConfigurationChanged()`.  
This method is passed a Configuration object that specifies the new device configuration.    
By reading fields in the Configuration, you can determine the new configuration and make appropriate changes by updating the resources used in your interface.  
At the time this method is called, your activity's Resources object is updated to return resources based on the new configuration, so you can easily reset elements of your UI without the system restarting your activity.  

For example, the following `onConfigurationChanged()` implementation checks the current device orientation:  
```java
@Override
public void onConfigurationChanged(Configuration newConfig) {
    super.onConfigurationChanged(newConfig);
    // Checks the orientation of the screen
    if (newConfig.orientation == Configuration.ORIENTATION_LANDSCAPE) {
        Toast.makeText(this, "landscape", Toast.LENGTH_SHORT).show();
    } else if (newConfig.orientation == Configuration.ORIENTATION_PORTRAIT){
        Toast.makeText(this, "portrait", Toast.LENGTH_SHORT).show();
    }
}
```


