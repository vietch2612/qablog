+++
date = "2015-12-23"
title = "Calabash: Calabash-iOS for iOS tutorial"
description = "How to use Calabash-iOS to Automated Test for iOS Application"
keywords = ["Calabash", "ios", "automation test", "testing", "quality control", "quality assurance"]
categories = ["Automation"]
+++
---
## Calabash iOS

[http://calaba.sh/](http://calaba.sh/)

Calabash is an automated testing technology for Android and iOS native and hybrid applications.

Calabash is a free-to-use open source project that is developed and maintained by [Xamarin](http://xamarin.com).

## Requirements

We recommend that you use the most recent released version of Xcode, MacOS, and Ruby.

* MacOS 10.10 or 10.11
* Xcode 6 or 7
* iOS Devices >= 7.1
* iOS Simulators >= 8.0
* ruby >= 2.0 (latest is preferred)

For the best Ruby experience we recommend that you use a managed Ruby
like [rbenv](https://github.com/sstephenson/rbenv) or [rvm](https://rvm.io/)).

If you are just getting started or don't want to commit to a managed Ruby, we
recommend you install and use the [Calabash Sandbox](https://github.com/calabash/install).

```
# Installs the Calabash Sandbox
$ curl -sSL https://raw.githubusercontent.com/calabash/install/master/install-osx.sh | bash
```

Please do *not* install gems with `sudo`

For more information about ruby on MacOS, see these Wiki pages:

* [Ruby on MacOS](https://github.com/calabash/calabash-ios/wiki/Ruby-on-MacOS)
* [Best Practice: Never install gems with sudo](https://github.com/calabash/calabash-ios/wiki/Best-Practice%3A--Never-install-gems-with-sudo)

## Getting Started

If you want to see Calabash iOS in action, head over to the [Calabash iOS Smoke Test App](https://github.com/calabash/ios-smoke-test-app) and follow the instructions in the README.  We use this app to document, demonstrate, and test Calabash iOS.  You can use this app to explore Calabash and as an example for how to configure your Xcode project and Calabash workflow.

The examples below assume you are using a managed ruby or are working in the Calabash
Sandbox:

```
$ calabash-sandbox
This terminal is now ready to use with Calabash.
To exit, type 'exit'.
```

### Step 1: Link calabash.framework

To start using Calabash in your project, you need to link an Objective-C framework (calabash.framework) to your application.  These instructions are compatible with apps
that are written in Swift.

|Tutorial|Description|
|:--------:|-----------|
|[Debug Config](https://github.com/calabash/calabash-ios/wiki/Tutorial%3A-Link-Calabash-in-Debug-config) | Use linker flags in the Debug build config to load the calabash.framework |
|[Calabash Config](https://github.com/calabash/calabash-ios/wiki/Tutorial%3A-Calabash-config) | Create a new Calabash Build Configuration |
|[-cal Target](https://github.com/calabash/calabash-ios/wiki/Tutorial%3A--Creating-a-cal-Target) | Add a new app target to Xcode.|

If you want to get started quickly, follow the [Debug Config](https://github.com/calabash/calabash-ios/wiki/Tutorial%3A-Link-Calabash-in-Debug-config) instructions.  The [Tutorial: How to add Calabash to Xcode](https://github.com/calabash/calabash-ios/wiki/Tutorial%3A-How-to-add-Calabash-to-Xcode) wiki page discusses the merits of each approach and has instructions for using CocoaPods.

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
