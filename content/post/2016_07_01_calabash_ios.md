+++
date = "2016-01-23"
title = "Calabash: Hướng dẫn cách cài đặt để kiểm thử ứng dụng iOS tự động với Calabash"
description = "Hướng dẫn sử dụng Calabash-iOS để kiểm thử ứng dụng iOS"
keywords = ["Calabash", "ios", "automation test", "testing", "quality control", "quality assurance"]
categories = ["Automation"]
+++
---
## Giới thiệu về Calabash

[http://calaba.sh/](http://calaba.sh/)

Giới thiệu về Calabash
Calabash là một ứng dựng nguồn mở và miễn phí để kiểm thử tự động các ứng dụng di động. Nó là ứng dụng đa nền tảng và hỗ trợ cả iOS và Android. Calabash bao gồm những thư viện cho phép tương tác với các native app và hybrid app giống như người dùng cuối bao gồm các hành động như giả lập cử chỉ, xác định đúng sai và chụp hình màn hình…

Bài lần trước chúng ta đã làm quen với Calabash cho Android và lần này chúng ta sẽ làm quen với iOS.

## Yêu cầu

Calabash khuyến khích bạn nên dùng phiên bản mới nhất của Xcode, MacOS và Ruby
* MacOS 10.10 or 10.11
* Xcode 6 or 7
* iOS Devices >= 7.1
* iOS Simulators >= 8.0
* ruby >= 2.0 (Hoặc version mới nhất nào bạn ưa thích)

Giống như bài trước, chúng ta sẽ dùng `rbenv` để quản lý Ruby: [rbenv](https://github.com/sstephenson/rbenv).
Và bây giờ cài đặt Calabash iOS
```bash
gem install calabash-ios
```

Hoặc bạn có thể dùng [Calabash Sandbox](https://github.com/calabash/install) nếu bạn không muốn dùng một chương trình quản lý Ruby nào hết.
```
# Cài đặt Calabash Sandbox
$ curl -sSL https://raw.githubusercontent.com/calabash/install/master/install-osx.sh | bash
```

Nên nhớ, **không** cài đặt `gems` bằng `sudo`

Các bạn có thể đọc bài trước để xem thêm cách cài đặt `rbenv`:
[Kiểm thử tự động ứng dụng Android bằng Calabash](http://blog.siliconstraits.vn/kiem-thu-tu-dong-ung-dung-android-bang-calabash/)

## Bắt đầu

If you want to see Calabash iOS in action, head over to the [Calabash iOS Smoke Test App](https://github.com/calabash/ios-smoke-test-app) and follow the instructions in the README.  We use this app to document, demonstrate, and test Calabash iOS.  You can use this app to explore Calabash and as an example for how to configure your Xcode project and Calabash workflow.

The examples below assume you are using a managed ruby or are working in the Calabash
Sandbox:

```
$ calabash-sandbox
This terminal is now ready to use with Calabash.
To exit, type 'exit'.
```

### Bước 1: Kết nối calabash.framework

Để bắt đầu Calabash trong dự án của bạn, bạn cần liên kết Objective-C framework (calabash.framework) vào trong ứng dụng của bạn. Dưới đây là hướng dẫn với ứng được iOS viết bằng ngôn ngữ Swift

### Step 2: Run Cucumber against an iOS Simulator

The [Calabash iOS Example](https://github.com/calabash/calabash-ios-example) README has simple instructions for how to link the calabash.framwork, generate a features directory, run cucumber, and and open a Calabash console.

```
# In the directory where your .xcodeproj and Gemfile are
$ bundle exec calabash-ios gen
```

Build and run in Xcode, targeting an iOS Simulator.  Calabash will try to detect the .app you just built.

```
$ bundle exec cucumber
```

If Calabash cannot find the .app you just built, it will raise an error.  If this happens, you will to tell Calabash where it can find your .app.

By default, Xcode builds to a DerivedData directory:

```
~/Library/Developer/Xcode/DerivedData/<UDID>/Build/Products/Debug-iphonesimulator/<NAME>.app
```

Try to locate the .app and set the `APP` variable:

```
$ export APP="~/Library/Developer/Xcode/DerivedData/<UDID>/Build/Products/Debug-iphonesimulator/<NAME>.app"
$ bundle exec cucumber
```

We recommend using scripts and/or changing the location where Xcode stages build products.  The sample projects use scripts to stage binaries to a `./Products`, even when building from Xcode.  You can use the Xcode > Preferences > Locations settings to do the same.

### Where to go from here?

| Topic | Description |
|-------|-------------|
| [Getting Started](https://github.com/calabash/calabash-ios/wiki/Getting-Started) | A more in-depth tutorial using the LPSimpleExample. |
| [Testing on Physical Devices](https://github.com/calabash/calabash-ios/wiki/Testing-on-Physical-Devices) | Everything you need to know about testing on physical devices. |
| [API Docs](http://calabashapi.xamarin.com/ios) | The Calabash iOS ruby API |
| [iOS Smoke Test App](https://github.com/calabash/ios-smoke-test-app) | Demonstrates advanced features, setups, and workflows|
| [iOS WebView Test App](https://github.com/calabash/ios-webview-test-app) | Demonstrates how to interact with UIWebView and WKWebView|
| [Getting Help](https://github.com/calabash/calabash-ios/wiki) | The Calabash iOS Wiki |
