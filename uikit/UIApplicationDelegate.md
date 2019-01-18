### UIApplicationDelegate
一系列被UIApplication调用的方法集。
https://developer.apple.com/documentation/uikit/uiapplicationdelegate


App delegate的角色：
* It contains your app’s startup code.

* It responds to key changes in the state of your app. Specifically, it responds to both temporary interruptions and to changes in the execution state of your app, such as when your app transitions from the foreground to the background.

* It responds to notifications originating from outside the app, such as low-memory warnings, download completion notifications, and more.

* It determines whether state preservation and restoration should occur and assists in the preservation and restoration process as needed.

* It responds to events that target the app itself and are not specific to your app’s views or view controllers.

* You can use it to store your app’s central data objects or any content that does not have an owning view controller.

#### Starting Up Your App

* Look at the launch options dictionary to determine why your app was launched. The application(_:willFinishLaunchingWithOptions:) and application(_:didFinishLaunchingWithOptions:) methods provide a dictionary with keys indicating the reason that your app was launched.

* Determine whether state restoration should proceed. If the app previously saved the state of its view controllers, restoration of those view controllers to their previous state proceeds only if the app delegate’s application(_:shouldRestoreApplicationState:) method returns true.

* Register for any remote notifications your app supports. In order to receive remote notifications (also known as push notifications), an app must register with the remote notification service by calling the registerForRemoteNotifications(matching:) method of the UIApplication object. Usually, you perform this task at launch time.

* Open a URL that was sent to your app. If there is a URL to open, the system calls the application(_:open:options:) method of your app delegate. You can also tell if there is a URL to open by looking in the launch options dictionary for the url key. You must declare the types of URLs your app supports by adding the CFBundleURLTypes key to your app’s Info.plist file. For more information about registering and handling URLs, see App Programming Guide for iOS.

* Provide the root window object for your app. Technically, the app delegate provided by Xcode already implements the window property, so you do not have to do anything special here unless you want to customize your app’s window.

#### Managing State Transitions
* Launch time:
application(_:willFinishLaunchingWithOptions:)
application(_:didFinishLaunchingWithOptions:)

* Transitioning to the foreground:
applicationDidBecomeActive()

* Transitioning to the background:
applicationDidEnterBackground()

* Transitioning to the inactive state:
applicationWillResignActive() (Called when leaving the foreground state.)
applicationWillEnterForeground() (Called when transitioning out of the background state.)

* Termination:
applicationWillTerminate() (Called only when the app is running. This method is not called if the app is suspended.)

... 
<font color="red">LaunchOptionsKey的应用场景</font>