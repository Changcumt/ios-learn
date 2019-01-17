### App生命周期

链接：https://developer.apple.com/documentation/uikit/core_app/managing_your_app_s_life_cycle

生命周期介绍：
UIKit apps are always in one of five states, which are shown in Figure 1. Apps start off not running. When the user explicitly launches the app, the app moves briefly to the inactive state before entering the active state. (An active app appears onscreen and is known as a foreground app.) Quitting an active app moves it offscreen and into the background state, where it stays until the system suspends it a short time later. At its discretion, the system may quietly terminate a suspended app, returning it to the not running state.

生命周期有5种状态 not runing,inactive,active,background,suspend. 周期从not runing开始，用户打开app，状态先变成inactive，等加载完资源，变成active，当一个active的app不显示在当前屏幕的时候状态变成background，直到系统暂停这个app 变成suspend， 系统有时候会自己终止app,使得状态变成not running

#### 生命周期事件
通过UIApplicationDelegate协议可以监听状态变化。
有5种生命周期事件：
1, Launch： 由not runinng 变成 inactive 或者 background。用这个事件来准备app运行
2, Activation: 由inactive变成active. app准备在前端显示
3, Deactivation: 由active变成inactive
4, Background execution：由inactive 或者not running变成background。要准备处理一些在屏幕背后的工作任务。
5, Termination： 从任何running状态到not running状态。

#### 其他行为事件
1, Memory warnings：减少app的使用内存。
2, Time changes： 更新时间
3, Protected data becomes available/unavailable. Manage files when the user locks or unlocks the device.
4, State restoration： 恢复之前的状态，
5, Handoff tasks. Continue tasks started on another device.
6, Open URLs. Receive and open URLs sent to your app.
7, Inter-app communication. Receive data from a paired watchOS app.
8, File downloads. Receive files that your app downloaded using a URLSession object.