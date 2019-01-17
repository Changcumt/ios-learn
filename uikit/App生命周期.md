### App生命周期

链接：https://developer.apple.com/documentation/uikit/core_app/managing_your_app_s_life_cycle

生命周期介绍：
UIKit apps are always in one of five states, which are shown in Figure 1. Apps start off not running. When the user explicitly launches the app, the app moves briefly to the inactive state before entering the active state. (An active app appears onscreen and is known as a foreground app.) Quitting an active app moves it offscreen and into the background state, where it stays until the system suspends it a short time later. At its discretion, the system may quietly terminate a suspended app, returning it to the not running state.

生命周期有5种状态 not runing,inactive,active,background,suspend. 周期从not runing开始，用户打开app，状态先变成inactive，等加载完资源，变成active，当一个active的app不显示在当前屏幕的时候状态变成background，直到系统暂停这个app 变成suspend， 系统有时候会自己终止app,使得状态变成not running

#### 生命周期事件
通过UIApplicationDelegate协议可以监听状态变化。
有5种生命周期事件：
1. Launch： 由not runinng 变成 inactive 或者 background。用这个事件来准备app运行
2. Activation: 由inactive变成active. app准备在前端显示
3. Deactivation: 由active变成inactive
4. Background execution：由inactive 或者not running变成background。要准备处理一些在屏幕背后的工作任务。
5. Termination： 从任何running状态到not running状态。

#### 其他行为事件
1. Memory warnings：减少app的使用内存。
2. Time changes： 更新时间
3. Protected data becomes available/unavailable. Manage files when the user locks or unlocks the device.
4. State restoration： 恢复之前的状态，
5. Handoff tasks. Continue tasks started on another device.
6. Open URLs. Receive and open URLs sent to your app.
7. Inter-app communication. Receive data from a paired watchOS app.
8. File downloads. Receive files that your app downloaded using a URLSession object.

#### Responding to the Launch of Your App 响应App启动
要做的事情：
* Perform any one-time setup required when your app is launched for the first time.
* nitialize your app's data structures.
* Configure the views and view controllers of your UI.
* Validate your app's content.
* Start any tasks that your app requires to run. For example, connect to the network resources that you need.

<font color="red">Use the keys in the launch options dictionary to understand why your app was launched and to provide an appropriate response. The dictionary should contain only keys that you expect to be there.</font>

launch steps:
1. The app is launched, either explicitly by the user or implicitly by the system.

2. The Xcode-provided main function calls UIKit's UIApplicationMain() function.

3. The UIApplicationMain() function creates the UIApplication object and your app delegate.

4. UIKit loads your app's default interface from the main storyboard or nib file.

5. UIKit calls your app delegate's application(_:willFinishLaunchingWithOptions:) method.

6. UIKit performs state restoration, which calls additional methods of your app delegate and view controllers.

7. UIKit calls your app delegate's application(_:didFinishLaunchingWithOptions:) method .

#### Preparing Your App to Run in the Foreground 准备在前端显示

When your app is launched, UIKit calls your app delegate’s applicationDidBecomeActive() method to let you know that your app is now active—that is, in the foreground. (If your app was already running in the background, UIKit calls the applicationWillEnterForeground() method before calling the applicationDidBecomeActive() method.) When your app is activated, you may start any app-specific tasks that you need when running in the foreground. For example:

* Start or resume any dispatch queues that you use to execute tasks.

* Make changes to your app's user interface.

* Start timers for periodic tasks.

When your applicationDidBecomeActive() method returns, UIKit shows any windows that you made visible. It also notifies any relevant view controllers that their views are about to appear. Use your view controller’s viewWillAppear() method to update the content of your views. For example, assign values to text fields and set the state of controls. (Don’t try to show a different view controller.) After your interface is onscreen, use your view controller’s viewDidAppear() method to:

* Start animations.

* Begin playing media files, if auto-play is enabled.

* Begin updating graphics for games and immersive content at their full frame rates.

<font color="red">Processing Queued Notifications 相关</font>

#### Preparing Your App to Run in the Background

When a foreground app moves to the background, UIKit first calls the applicationWillResignActive(_:) method to deactivate the app. When deactivation occurs, do the following.

* Save user data to disk and close any open files. Always save user data in case your app needs to be terminated. Close files in case the user locks the device.

* Do only work that’s critical to preserving the user’s data. Pause dispatch queues and operation queues, and don’t schedule any new tasks for execution.

* Invalidate any active timers.

* Pause gameplay. Deactivation prevents the user from interacting with your app anyway.

For a foreground app that is moving to the background, UIKit follows deactivation with a call to the applicationDidEnterBackground() method of your app delegate. This method signals that your app is now running in the background. When transitioning to the background, you might take some additional steps before your app is suspended.

* Clean up your app’s user interface. Hide sensitive information, dismiss alerts and other temporary interfaces, and prepare your interface to have its snapshot taken.

* Release shared system resources. The foreground app has priority for using shared services like the camera or system databases. At the time when an app would be suspended, if the app is holding any shared resources, the system terminates it instead.

* Cancel Bonjour–related services. Unregister from Bonjour and close any listening sockets that you use for your services. If your app becomes suspended, it cannot respond to requests anyway.

* Release images, media files, and temporary objects. Remove references to any large, in-memory objects that can be easily recreated or reloaded from disk. The system automatically empties system-managed caches, including data managed by NSCache objects and objects that adopt the NSDiscardableContent protocol.

其他几个知识点
* [Updating Your App with Background App Refresh 后台更新数据](https://developer.apple.com/documentation/uikit/core_app/managing_your_app_s_life_cycle/preparing_your_app_to_run_in_the_background/updating_your_app_with_background_app_refresh)

* [延长后台运行时间](https://developer.apple.com/documentation/uikit/core_app/managing_your_app_s_life_cycle/preparing_your_app_to_run_in_the_background/extending_your_app_s_background_execution_time)

* [About the Background Execution Sequence](https://developer.apple.com/documentation/uikit/core_app/managing_your_app_s_life_cycle/preparing_your_app_to_run_in_the_background/about_the_background_execution_sequence)