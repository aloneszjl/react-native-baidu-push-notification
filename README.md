# react-native-baidu-push-notification

## Getting started

`$ npm install react-native-baidu-push-notification --save`

### Mostly automatic installation

`$ react-native link react-native-baidu-push-notification`

### Manual installation

### iOS manual Installation

The component uses PushNotificationIOS for the iOS part.

[Please see: PushNotificationIOS](https://facebook.github.io/react-native/docs/pushnotificationios.html#content)

#### Android

if you already run react-native link react-native-baidu-push-notification, skip step 1,2,3

1. Open up `android/app/src/main/java/[...]/MainApplication.java`

   - Add `import com.alones.reactnative.baidupush.ReactNativePushNotificationPackage;` to the imports at the top of the file
   - Add `new ReactNativePushNotificationPackage()` to the list returned by the `getPackages()` method

2. Append the following lines to `android/settings.gradle`:
   ```
   include ':react-native-baidu-push-notification'
   project(':react-native-baidu-push-notification').projectDir = new File(rootProject.projectDir, 	'../node_modules/@beesight/react-native-baidu-push-notification/android')
   ```
3. Insert the following lines inside the dependencies block in `android/app/build.gradle`:
   ```
     compile project(':react-native-baidu-push-notification')
   ```
4. Open up `android/app/src/main/AndroidManifest.xml` add uses-permissions

   ```
   <uses-permission android:name="baidu.push.permission.WRITE_PUSHINFOPROVIDER.your_package_name" />
   ```

   Add permissions to access push notification (replace your app package):

   ```
    <permission
        android:name="baidu.push.permission.WRITE_PUSHINFOPROVIDER.your_package_name"
        android:protectionLevel="normal">
    </permission>
   ```

   Under `<application>` (replace your app package)

   ```
    <provider
            android:name="com.baidu.android.pushservice.PushInfoProvider"
            android:authorities="your_package_name.bdpush"
            android:exported="true"
            android:protectionLevel="signature"
            android:writePermission="baidu.push.permission.WRITE_PUSHINFOPROVIDER.your_package_name" />
   ```

   ```
    <meta-data
            android:name="baidu_push_api_key"
            android:value="your_api_key" />
   ```

5. copy `node_modules/react-native-baidu-push-notification/android/jniLibs` to `android/app/src/main/jniLibs`

## Usage

```javascript
import RNPushNotification from "react-native-baidu-push-notification";

// TODO: What to do with the module?
componentDidMount() {
	PushNotification.configure({
      popInitialNotification: Platform.select({
        ios: false,
        android: true,
      }),
      onRegister(data) {
        const token = get(data, 'token');
        if (token) {
          console.log('yout device token:',token)
        }
      },
      onNotification: this.handlePushNotification,
    });
}

handlePushNotification = notification => {
	console.log(notification)
}
```
