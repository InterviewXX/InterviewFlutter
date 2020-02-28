# App

## WidgetsBindingObserver

```text
abstract class WidgetsBindingObserver {
  //页面pop
  Future<bool> didPopRoute() => Future<bool>.value(false);
  //页面push
  Future<bool> didPushRoute(String route) => Future<bool>.value(false);
  //系统窗口相关改变回调，如旋转
  void didChangeMetrics() { }
  //文本缩放系数变化
  void didChangeTextScaleFactor() { }
  //系统亮度变化
  void didChangePlatformBrightness() { }
  //本地化语言变化
  void didChangeLocales(List<Locale> locale) { }
  //App生命周期变化
  void didChangeAppLifecycleState(AppLifecycleState state) { }
  //内存警告回调
  void didHaveMemoryPressure() { }
  //Accessibility相关特性回调
  void didChangeAccessibilityFeatures() {}
}
```

可以通过 [WidgetsBinding.addObserver](https://api.flutter.dev/flutter/widgets/WidgetsBinding/addObserver.html) and [WidgetsBinding.removeObserver](https://api.flutter.dev/flutter/widgets/WidgetsBinding/removeObserver.html) 来添加或者移除监听。

## 生命周期回调

didChangeAppLifecycleState 回调函数中，有一个参数类型为 `AppLifecycleState` 的枚举类，这个枚举类是 Flutter 对 App 生命周期状态的封装。它的常用状态包括 resumed、inactive、paused 这三个。

* resumed：可见的，并能响应用户的输入。
* inactive：处在不活动状态，无法处理用户响应。
* paused：不可见并不能响应用户的输入，但是在后台继续活动中。

![&#x5207;&#x6362;&#x524D;&#x540E;&#x53F0;&#x5E94;&#x7528;&#x72B6;&#x6001;&#x53D8;&#x5316;&#x60C5;&#x51B5;](../../.gitbook/assets/image%20%283%29.png)

## 帧绘制回调

WidgetsBinding 提供了单次 Frame 绘制回调，以及实时 Frame 绘制回调两种机制，来分别满足不同的需求：

* 单次 Frame 绘制回调，通过 addPostFrameCallback 实现。它会在当前 Frame 绘制完成后进行进行回调，并且只会回调一次，如果要再次监听则需要再设置一次。

```text
WidgetsBinding.instance.addPostFrameCallback((_){
    print("单次Frame绘制回调");//只回调一次
  });
```

* 实时 Frame 绘制回调，则通过 addPersistentFrameCallback 实现。这个函数会在每次绘制 Frame 结束后进行回调，可以用做 FPS 监测、卡顿检测。

```text
WidgetsBinding.instance.addPersistentFrameCallback((_){
  print("实时Frame绘制回调");//每帧都回调
});
```

## 相关链接

[Flutter核心技术与实战：11 \| 提到生命周期，我们是在说什么？](https://time.geekbang.org/column/article/109490)

[WidgetsBindingObserver class](https://api.flutter.dev/flutter/widgets/WidgetsBindingObserver-class.html)

