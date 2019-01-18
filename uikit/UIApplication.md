### UIApplication

The centralized point of control and coordination for apps running in iOS
https://developer.apple.com/documentation/uikit/uiapplication

* UIApplication是单例，一个App一般只有一个。可以通过UIApplication.shared 来获取。
* 作用有：1 响应用户事件 2 管理路由 3 管理UIwindows，并通过他们来管理UIView 4 通知运行时事件 5 处理资源信息 如图片 Email等 6 管理设备特殊行为

#### 获取App实例
```
class var shared: UIApplication
```

#### 管理App行为
```
var delegate: UIApplicationDelegate  // 返回app的delegate
```
protocol [UIApplicationDelegate](UIApplicationDelegate.md) : UIApplication需要遵循的协议

#### 注册远程通知 Registering for Remote Notifications

* func registerForRemoteNotifications() //注册远程注册
Call this method to initiate the registration process with Apple Push Notification service. If registration succeeds, the app calls your app delegate object’s application(_:didRegisterForRemoteNotificationsWithDeviceToken:) method and passes it a device token. You should pass this token along to the server you use to generate remote notifications for the device. If registration fails, the app calls its app delegate’s application(_:didFailToRegisterForRemoteNotificationsWithError:) method instead.
* func unregisterForRemoteNotifications() //取消注册远程注册
* var isRegisteredForRemoteNotifications: Bool //判断当前app是否注册了远程通知

#### 获取App状态 Getting the Application State
* var applicationState: UIApplication.State { get } 
* UIApplication.State 是一个枚举 {active:0,inactive:1,background:2}

#### 管理后台运行情况 Managing Background Execution

* var backgroundRefreshStatus: UIBackgroundRefreshStatus { get } 指示app是否可以在后台运行任务。当设备低电量时 会自动禁止后台运行。
* enum UIBackgroundRefreshStatus {restricted:0,denied:1,available:2}
* beginBackgroundTask <font color="red">未学习</font>
* endBackgroundTask <font color="red">未学习</font>
* backgroundTimeRemaining <font color="red">未学习</font>

#### 后台获取内容 Fetching Content in the Background

#### 打开URL资源 Opening a URL Resource

#### 管理空闲时间 Managing the App Idle Timer

#### 管理状态恢复行为 Managing the State Restoration Behavior

#### 管理3Dtouch  Managing Home Screen Quick Actions for 3D Touch

#### 受保护内容的可获得性 Determining the Availability of Protected Content

#### 注册远程控制事件 Registering for Remote Control Events

#### 控制App外观 Controlling App Appearance

#### 控制和处理事件 Controlling and Handling Events

#### Managing the App's Icon

#### Getting App Windows

#### Getting the Font Sizing Preference

#### Managing the Default Interface Orientations

#### Managing Status Bar Animations

#### Constants 常量包括UIStatusbarStyle UIStateBarAnumation 等

#### Notifications 通知相关