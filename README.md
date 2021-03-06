# BobbleIMESDK

This guide is for all app developers who wish to add a custom keyboard functionality in their Android apps using the Bobble IME (Input Method Editor) SDK. Before you begin integrating the SDK into your app, please email us at android.master@bobble.ai to get the license key in order to avail complete functionalities of the SDK.

Note - Minimum version of supported Android platform is SDK level 21

### Step 1: Adding the BobbleIME SDK to your Project
##### Option 1: Pulling the Latest SDK via JCenter
If you are using Gradle to build your Android applications, you can pull the latest version of the SDK from JCenter as described below:

 - Include JCenter in your top-level build.gradle file:

```java
allprojects {
    repositories {
        jcenter()
    }
}
```
- Add the following line to the dependencies element in your application module’s build.gradle.

```java
implementation 'com.touchtalent.bobbleime:1.0.0'
```

- Sync your Gradle project to ensure that the dependency is downloaded by the build system.


##### Option 2: Adding the SDK Library to your Application Project

Alternatively, you can download the latest version of BobbleIME’s SDK and copy the library to your application module’s libs/ directory.

To add the library to your project’s dependencies, add this line to the dependencies element in your module’s <strong>build.gradle</strong>:

```java
implementation fileTree(dir: 'libs', include: ['*.aar'])
```


### Step 2: Adding Permissions
##### Granting Permissions

The SDK uses the permissions granted to your app in order to improve the typing experience, and in order to suggest the most relevant content to your users.
We highly recommend that your app request the following permissions so that we can personalise user experience in a better way:
```java
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.READ_CONTACTS" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
```
    
    
### Step 3: Manifest Changes
The client needs to register the custom IME class in manifest as InputMethod service.

```java
<service
    android:name=".CustomIME"
    android:label="<Add your keyboard name here>"
    android:permission="android.permission.BIND_INPUT_METHOD">
    <intent-filter>
        <action android:name="android.view.InputMethod" />
    </intent-filter>
</service>
```

### Step 4: Other Build Settings
- Add option to not compress dictionary files by following lines in the android block of your gradle
```java
aaptOptions {
	noCompress ".dict"
}
```

- Enable data binding for the SDK components to work by adding 
```java
dataBinding {
   enabled true
}
```

### Step 5: Initialise SDK
Inside onCreate() method of your Application class, initialise the SDK by calling
```java
BobbleIMESDK.initialise(applicationContext, <LICENSE_KEY>) 
```
If you don't have a Licence Key for your host app, you need to request one. Please note that Licence Key do not superimpose any expiration date, but each Licence Key is bounded to host app package name.

### Step 6: Create your custom IME Class
Last step would be to create the custom class declared in the manifest above.
```java
import com.bobblekeyboard.ime.BobbleIME;

class CustomIME extends BobbleIME {
    @Override
    public void onCreate() {
        super.onCreate();
    }
}
```



