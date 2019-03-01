>
> PLEASE NOTE: There are breaking changes with the release of 2.0. If continuing use of 1.x, please change your pod file to use: `pod 'Skafos', '1.0.1'` instead of `pod 'Skafos'`
>

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

  // Shorthand:
  Skafos.initialize("your project token", swizzle: true, debug: true)

  // Longhand:
  // Skafos.initialize(
  //   Config(
  //      token: "your project token",
  //      meta: ["Any meta data" : "you want"],
  //      swizzle: (true or false),
  //      isDev: (true or false)
  //   ) 
  // )

  // ...

  return true
}
```

Add push notification handlers and then the Skafos push handlers
> Note: If you set `swizzle` to `true` this is not needed.

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

Skafos.load(asset: "your asset name", version: "Asset version") { (error, asset) in
  if let error = error {
    print("Oh man, an error: \(error)")

    return
  }

  if let model = asset.model {
    self.classifier.model = model
  }

  for file in asset.files {
    print("File name: \(file.name) and path: \(file.path)")
  }

  // And if you have multiple MLModels you can always loop through those too:
  for model in asset.models {
    print("Model name: \(model.name), path: \(model.path), and model itself: \(model.model)")
  }
}

```

## License

Skafos swift framework uses the Apache2 license, located in the LICENSE file.

## Questions?

Contact us by email <a href="mailto:..">hello@skafos.io</a>, or by twitter @skafos.
