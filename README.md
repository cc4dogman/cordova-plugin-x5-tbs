# cordova-plugin-x5-tbs-flyhh

把``Cordova``的``WebView``替换为腾讯的[X5](http://x5.tencent.com/)。使用腾讯TBS完整版SDK。

## 优劣比较

### 优势
- 安装包体积小：由于QQ、微信、QQ空间等在中国的巨大装机量，与``Crosswalk``比较，``X5``内核仅增加不到300KB左右的``apk``大小。
- 兼容性强：统一不同设备到同一内核，不需要担心国产ROM奇特“定制”及老版本``WebView``造成的兼容性问题。
- 视频播放能力强：自带多种解码器，也可支持直播。
- 新浏览器特性支持：如HTTP/2、Service Worker等。

### 劣势
- [海外用户量：海外只能共享手机QQ的X5内核](http://x5.tencent.com/tbs/technical.html#/detail/sdk/1/14e9f3f4-ed64-4330-8e31-25d1f1a68cf7)
- Google Play上架风险：需要使用精简版本SDK，否则可能不予上架。

## 支持环境

- cordova-android > 6.4
- Android > 4.0

## 安装

``cordova plugin add cordova-plugin-x5-tbs-flyhh``

为确保App启动后即启动X5内核，需要在项目的``MainActivity``的``onCreate``方法内，增加以下代码：

```java
QbSdk.initX5Environment(this, null);
```

同时也要import下 import com.tencent.smtt.sdk.QbSdk;



安装好插件后会自动的添加权限到AndroidManifest.xml，如应用出现Crash，请检查并手动将以下权限复制入AndroidManifest.xml

```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.READ_SETTINGS" />
<uses-permission android:name="android.permission.WRITE_SETTINGS" />
<uses-permission android:name="android.permission.MOUNT_UNMOUNT_FILESYSTEMS" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<!-- 硬件加速对X5视频播放非常重要，建议开启 -->
<uses-permission android:name="android.permission.GET_TASKS" />
```

## 卸载

``cordova plugin rm cordova-plugin-x5-tbs-flyhh``

## 环境

### 当前版本

X5：tbs_sdk_thirdapp_v4.3.0.1020_43633_sharewithdownload_withoutGame_obfs_20190111_105200.jar（此版本可以直接在vscode中进行debug了，无需TBS Stdio）

## 内核替换

你当然可以手动升级到X5内核最新版，或者替换成精简版内核。你只需要删除``platforms/android/libs/tbs_sdk_*.jar``，替换为你需要使用的版本即可。这会使此插件无法通过``cordova plugin remove``等指令被完全删除，还请注意（PS：也可以使用同一名称直接替换，这样指令都正常）。


## 感谢

此项目继承自项目：[cordova-plugin-x5-tbs](https://github.com/zsxsoft/cordova-plugin-x5-tbs)

## 技术支持

与本项目有关的问题，如加载后无法正常启动，在本项目Issue区内提交新Issue即可。

X5相关问题，请参阅：[X5技术指南](http://x5.tencent.com/tbs/guide.html)

### 常见玄学问题

#### 为什么X5内核没有被成功加载

请使用官方TBS Studio测试，如其安装的TBS Demo左上角仍显示``Sys core``，证明X5内核可能无法被第三方App调用。请参阅X5技术指南或反馈到X5官方。
