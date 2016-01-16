+++
date = "2016-01-17"
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
## Cài đặt

Để bắt đầu Calabash trong dự án của bạn, bạn cần liên kết Objective-C framework (calabash.framework) vào trong ứng dụng của bạn. Dưới đây là hướng dẫn với ứng được iOS viết bằng ngôn ngữ Swift

#### Tại sao phải chia riêng biệt Target ra?

Tại vì Calabash có chưa framework và methods mà khi thêm vào project của bạn có thể bị reject bởi AppStore.

### Bước 1. Tạo Calabash target
#### 1.1 Tạo bản sao target từ Production
Trong list target, chuột phải vào Production target và chọn `Duplicate`
![Duplicate target](http://i.imgur.com/l1iau88.jpg)

Nếu project của bạn chỉ dành cho iPhone hay iPad thì bạn sẽ nhìn thấy thông báo như này:
![Alert](http://i.imgur.com/VLoZHHw.png)
Nếu có, hãy chọn "Duplicate Only"

#### 1.2 Đổi tên cho Target vừa tạo
![Rename target](http://i.imgur.com/6d6ZgjV.jpg)
Bạn nên đổi tên theo dạng `tênapp-cal`

#### 1.3 Thay đổi bundle identifier
![Rename bundle](http://i.imgur.com/WFvsKgC.jpg)

#### 1.4 Thay đổi Info.plist
![Change info.plist](http://i.imgur.com/VEtyYlc.jpg)
Là Info.plist của target Production

#### 1.5 Xoá Info.plist bản copy khi Duplicate target từ Production
![Remove info.plist](http://i.imgur.com/spK8bMR.jpg)

### Bước 2. Tạo Calabash Schema
#### 2.1 Chọn Schema -> Manage Schema
![ManageSchema](http://i.imgur.com/UJ34NpB.jpg)

#### 2.2 Đổi tên của Schema copy
![DuplicateSchema](http://i.imgur.com/neKWHsK.jpg)

#### 2.3 Đánh dấu `Show` và `Shared`
![Check shared](http://i.imgur.com/tOlm8Hg.jpg)

#### 2.4 Chọn Scheme Executable
Bước này có thể không cần thiết nhưng bạn cần phải chắc chắn rằng Executable cho -cal scheme là -cal target.
![exe](http://i.imgur.com/dOxEnIG.jpg)

### Bước 3. Link tới CFNetwork.framework
![link](http://i.imgur.com/vU5J0xd.jpg)
![cfnetwork](http://i.imgur.com/GbVurI3.jpg)

### Bước 4. Link tới calabash.framework
#### 4.1 Tải về calabash.framework

Tạo Gemfile trong folder chứa file .xcodeproj của bạn với nội dung sau:
```Bash
source "https://rubygems.org"
gem "calabash-cucumber", ">= 0.16", "< 2.0"
```
Và chạy những câu lệnh sau đây tại thư mục đó
```bash
bundle
```
```bash
bundle exec calabash-ios download
```
Nếu màn hình kết quả trả về kết quả như sau nghĩa là đã hoàn thành
```bash
----------Info----------
caution: excluded filename not matched:  __MACOSX/*
caution: excluded filename not matched:  calabash.framework/.DS_Store
---------------------------
```

#### 4.2 Thêm calabash.framework vào project
Hãy chắc chắn rằng calabash-framework không được trỏ tới target nào hết.
![add f](http://i.imgur.com/wrMa9mf.jpg)
![add f](http://i.imgur.com/isStJZD.jpg)
![no target](http://i.imgur.com/7NKMT5I.jpg)

#### 4.3 Link tới calabash.framework
![link](http://i.imgur.com/XhYWywr.jpg)

Thêm đoạn sau vào Other Linked Flags
```bash
-ObjC -force_load "$(SOURCE_ROOT)/calabash.framework/calabash"
```
## Chạy test Cucumber trên iOS Simulator

Khởi tạo feature folder

```
# Trong folder chứa file .xcodeproj và Gemfile
$ bundle exec calabash-ios gen
```

Build và run trong Xcode, chọn target tới iOS Simulator.  Calabash sẽ tự động tìm file .app bạn vừa build.
Và chúng ta run test:

```
$ bundle exec cucumber
```

Nếu Calabash không tìm thấy file .app bạn vừa build thì Calabash sẽ báo lỗi "Cannot find APP_BUNDLE_PATH". Nếu nó sảy ra thì bạn hãy tạo biến môi trường APP_BUNDLE_PATH bằng tay

Khi build thì mặc định file .app của bạn sẽ nằm tại:

```
~/Library/Developer/Xcode/DerivedData/<UDID>/Build/Products/Debug-iphonesimulator/<NAME>.app
```

và tạo biến môi trường `APP_BUNDLE_PATH`:

```
$ export APP="~/Library/Developer/Xcode/DerivedData/<UDID>/Build/Products/Debug-iphonesimulator/<NAME>.app"
$ bundle exec cucumber
```

Còn tất cả các bước khác như Define steps, report thì đều giống Calabash Android trong bài viết trước mình đã đề cập. Hy vọng bài viết sẽ giúp bạn có thêm 1 lựa chọn mới để giúp công việc của bạn trở nên thú vị và giảm được thời gian. Cảm ơn.
