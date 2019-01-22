<h1 align="center">SKAFOS</h1>

<p align="center">
    <a href="#installation">Installation</a>
  • <a href="#usage">Usage</a>
  • <a href="#license">License</a>
  • <a href="#questions">Questions?</a>
</p>

Skafos seeks to free you from the tedious tasks and unnecessary work to just try a machine learning models in your app. Why does it have to be so hard?!  Well it doesn't.  This guide will get you from zero to AI hero in no time - and once you are done with this guide, you will have an app that uses ML.  Where you take it from here is up to you, however we are here to help you every step of the way. 

---

## Installation
1. Sign up for Skafos account at [Skafos](https://skafos.io)
2. Create a ML project using Skafos dashboard at [Quickstart](http://dashboard.metismachine.io/quickstart/project)
3. Configure your app to use Skafos, including enable background updates via push notifications.
4. Add `pod 'skafos'` to your `Podfile` and `pod install`

---

## Usage
Inside your app delegate, add the following:

```swift
import Skafos
```

Then configure the framework with your project token:

```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
  // ...

  Skafos.configure("YOUR PROJECT TOKEN")

  // ...

  return true
}
```

Add push notification handlers and then the Skafos push handlers

```swift

func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
  Skafos.application(application, didRegisterForRemoteNotificationsWithDeviceToken: deviceToken)
}

func application(_ application: UIApplication, didFailToRegisterForRemoteNotificationsWithError error: Error) {
  Skafos.application(application, didFailToRegisterForRemoteNotificationsWithError: error)
}

func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
  Skafos.application(application, didReceiveRemoteNotification: userInfo, fetchCompletionHandler: completionHandler)
}

func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) {
  Skafos.application(application, didReceiveRemoteNotification: userInfo)
}

```


Now you are all set to call Skafos and ask it to load your model.

```swift

Skafos.load(savedModel) { model in
  guard let model = model else { return }
  
  self.classifier.model = model
}

```

## License

Skafos swift framework uses the Apache2 license, located in the LICENSE file.

## Questions?

Contact us by email <a href="mailto:..">hello@skafos.io</a>, or by twitter @skafos.
