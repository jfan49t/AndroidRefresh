- [1. Activity](#1-activity)
  - [1.0. AndroidManifest.xml](#10-androidmanifestxml)
  - [1.0.1 Intents and Intent Filters](#101-intents-and-intent-filters)
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
Intent filters

App activities, services, and broadcast receivers are activated by intents. An intent is a message defined by an Intent object that describes an action to perform, including the data to be acted upon, the category of component that should perform the action, and other instructions.

When an app issues an intent to the system, the system locates an app component that can handle the intent based on intent filter declarations in each app's manifest file. The system launches an instance of the matching component and passes the Intent object to that component. If more than one app can handle the intent, then the user can select which app to use.

An app component can have any number of intent filters (defined with the <intent-filter> element), each one describing a different capability of that component.

## 1.0.1 Intents and Intent Filters

An Intent is a messaging object you can use to request an action from another app component. Although intents facilitate communication between components in several ways, there are three fundamental use cases:

- Starting an activity
- Starting a service
- Delivering a broadcast

Explicit intents specify which application will satisfy the intent, by supplying either the target app's package name or a fully-qualified component class name. You'll typically use an explicit intent to start a component in your own app, because you know the class name of the activity or service you want to start. For example, you might start a new activity within your app in response to a user action, or start a service to download a file in the background.

Implicit intents do not name a specific component, but instead declare a general action to perform, which allows a component from another app to handle it. For example, if you want to show the user a location on a map, you can use an implicit intent to request that another capable app show a specified location on a map.

```
val sendIntent = Intent(Intent.ACTION_SEND)
...

// Always use string resources for UI text.
// This says something like "Share this photo with"
val title: String = resources.getString(R.string.chooser_title)
// Create intent to show the chooser dialog
val chooser: Intent = Intent.createChooser(sendIntent, title)

// Verify the original intent will resolve to at least one activity
if (sendIntent.resolveActivity(packageManager) != null) {
    startActivity(chooser)
}

```

Receiving an implicit intent

```
<activity android:name="ShareActivity">
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <data android:mimeType="text/plain"/>
    </intent-filter>
</activity>

```

Caution: Using an intent filter isn't a secure way to prevent other apps from starting your components. Although intent filters restrict a component to respond to only certain kinds of implicit intents, another app can potentially start your app component by using an explicit intent if the developer determines your component names. If it's important that only your own app is able to start one of your components, do not declare intent filters in your manifest. Instead, set the exported attribute to "false" for that component.

Similarly, to avoid inadvertently running a different app's Service, always use an explicit intent to start your own service.


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