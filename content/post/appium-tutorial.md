+++
date = "2015-12-23"
title = "Appium: Appium for Android tutorial"
description = "How to use Appium to Automated Test for Android Application"
keywords = ["appium", "android", "automation test", "testing", "quality control", "quality assurance"]
categories = ["Automation"]
+++
---

### Các phần mềm yêu cầu. (Dành cho Windows)
1. Java JDK [http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html)
2. Android SDK [https://developer.android.com/sdk/index.html](https://developer.android.com/sdk/index.html)
3. Appium Desktop Apps [http://appium.io/downloads.html](http://appium.io/downloads.html)
4. Phầm mềm giả lập Android hoặc một chiếc device chạy Android thật. Yêu cầu phải có API >= 17 (4.2). Mình gợi ý dùng Genymotion vì khá là nhẹ với những bạn có PC cấu hình yếu. [https://www.genymotion.com/](https://www.genymotion.com/)
5. Java IDE (IntelliJ, Eclipse, Netbeans ...). Tại bài hướng dẫn này thì mình sử dụng IntelliJ 14 https://www.jetbrains.com/idea/download/

### Các bước tiến hành
1. Cài đặt Java JDK.
Tiến hành cài đặt như bình thường và tạo biến môi trường: JAVA_HOME. Hướng dẫn có sẵn tại đây https://confluence.atlassian.com/doc/setting-the-java_home-variable-in-windows-8895.html

2. Android SDK: Cài đặt và tải SDK Packages mới nhất. Hướng dẫn có sẵn tại đây https://developer.android.com/sdk/installing/adding-packages.html. Sau khi cài đặt xong sẽ tạo thêm biến môi trường ANDROID_HOME.

3. Cài đặt Appium và chạy Appium.exe, nhấn nút Start để start appium server.

4. Tạo một Android Emulator hoặc tìm một device thật để test.

### Tạo một project mới
Hướng dẫn này sử dụng IntelliJ IDEA và test trên Whatsapp.apk

Từ IntelliJ, tạo một Maven Project mới.

Trong pom.xml, add thêm 2 dependencies là io.appium và testNG

>     <dependencies>
>         <dependency>
>             <groupId>io.appium</groupId>
>             <artifactId>java-client</artifactId>
>             <version>3.1.0</version>
>         </dependency>
>         <dependency>
>             <groupId>org.testng</groupId>
>             <artifactId>testng</artifactId>
>             <version>6.9.6</version>
>         </dependency>
>     </dependencies>

### Tạo một class Test cơ bản.
