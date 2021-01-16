- [1. Activity](#1-activity)
  - [1.0. AndroidManifest.xml](#10-androidmanifestxml)
  - [1.1. Handle configuration changes](#11-handle-configuration-changes)
  - [1.2.](#12)
- [2. Services](#2-services)
- [3. BroadcastReciver](#3-broadcastreciver)
- [4. CountenProvider](#4-countenprovider)
# 1. Activity

## 1.0. AndroidManifest.xml

a.The app's package name and version.

b.The components of the app.

c.The permissions.

d.The hardware and software features the app requires, 
```
<manifest ... >
    <uses-feature android:name="android.hardware.sensor.compass"
                  android:required="true" />
    ...
</manifest>
```

App components

For each app component that you create in your app, you must declare a corresponding XML element in the manifest file:

```
<activity> for each subclass of Activity.
<service> for each subclass of Service.
<receiver> for each subclass of BroadcastReceiver.
<provider> for each subclass of ContentProvider.

```

## 1.1. Handle configuration changes
Some device configurations can change during runtime (such as screen orientation, keyboard availability, and when the user enables multi-window mode).

When such a change occurs, Android restarts the running Activity ( onDestroy() is called, followed by onCreate()).
 
a.onSaveInstanceState() with Bundle (it is not designed to carry large objects (such as bitmaps) and the data within it must be serialized then deserialized on the main thread, which can consume a lot of memory and make the configuration change slow ), ViewModels, and persistent storage)

b.Handle the configuration change yourself
```
<activity android:name=".MyActivity"
          android:configChanges="orientation|screenSize|screenLayout|keyboardHidden"
          android:label="@string/app_name">

```
Now, when one of these configurations change, MyActivity does not restart. Instead, the MyActivity receives a call to onConfigurationChanged().

## 1.2. 


# 2. Services
# 3. BroadcastReciver
# 4. CountenProvider