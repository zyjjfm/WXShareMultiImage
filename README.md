# WXShareMultiImage

基于无障碍服务实现微信多图分享。

[ ![Download](https://api.bintray.com/packages/shichaohui/maven/wx-share/images/download.svg) ](https://bintray.com/shichaohui/maven/wx-share/_latestVersion)

## 功能

* 分享多图+文字给好友。
* 分享多图+文字到朋友圈。
* 可自定义引导用户打开无障碍服务的弹窗。

[下载Demo](./demo.apk)

## Gradle 依赖

```groovy
implementation 'com.sch.share:wx-share:1.0.7'
```

## 配置

在 strings.xml 中自定义无障碍服务标签。
```xml
<string name="wx_share_multi_image_service_label">ShareDemo【多图分享】</string>
```

## 权限

由于 SDK 涉及文件操作，请添加相关权限。
```
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
```

## API

[查看所有 API 。](./wx-share/src/main/java/com/sch/share/WXShareMultiImageHelper.kt)

![API](./api.png)

## 用法：

### 分享给好友

```
/*
 * bitmapList: List<Bitmap> 待分享图片列表。
 * text: String 待分享文案。
 */

WXShareMultiImageHelper.shareToSession(activity, bitmapList)

WXShareMultiImageHelper.shareToSession(activity, bitmapList, text)
```

### 分享到朋友圈

```
/*
 * bitmapList: List<Bitmap> 待分享图片列表。
 * text: String 待分享文案。
 * isAuto: Boolean false 表示由用户手动粘贴文字、选择选图，不会执行无障碍操作；
 *                 true 表示使用无障碍操作（弹窗引导用户打开无障碍服务，若用户不打开，将和 false 等同）。
 *                 默认为 true 。
 */

WXShareMultiImageHelper.shareToTimeline(activity, bitmapList)

WXShareMultiImageHelper.shareToTimeline(activity, bitmapList, text)

WXShareMultiImageHelper.shareToTimeline(activity, bitmapList, text, isAuto)
```
分享时默认 isAuto 为 true，即会尝试使用无障碍服务，若无障碍服务未打开，会弹出提示框引导用户打开服务。
如果不想使用默认的弹窗，可以自行弹窗引导用户打开服务，并将结果作为 `shareToTimeline()` 的 isAuto 参数 。

### 清理临时文件

分享时会产生临时文件，每次分享前都会自动清理临时所属文件夹，也可以在特定时间调用 API 清理。

```
WXShareMultiImageHelper.clearTmpFile(activity)
```

### 判断无障碍服务是否可用

```
if(WXShareMultiImageHelper.isServiceEnabled(activity)) {
    // do something.
} else {
    // do something.
}
```

### 打开无障碍服务

```
// Kotlin
WXShareMultiImageHelper.openService(activity) {
    // 结果回调，it: Boolean 表示是否打开了无障碍服务。
    isServiceEnabled = it
}

// Java
WXShareMultiImageHelper.openService(activity, new WXShareMultiImageHelper.OnOpenServiceListener() {
    @Override
    public void onResult(boolean isOpen) {
        // do something.
    }
});
```

# License

```
 Copyright 2018 StoneHui
 
 Licensed under the Apache License, Version 2.0 (the "License");
 you may not use this file except in compliance with the License.
 You may obtain a copy of the License at
 
      http://www.apache.org/licenses/LICENSE-2.0
 
 Unless required by applicable law or agreed to in writing, software
 distributed under the License is distributed on an "AS IS" BASIS,
 WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 See the License for the specific language governing permissions and limitations under the License.
 ```
