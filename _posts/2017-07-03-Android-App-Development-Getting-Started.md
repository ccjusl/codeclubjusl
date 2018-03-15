---
title: Android App Development - Getting Started
layout: post
comments: true
date: '2017-07-03'
---

<img src="images/Android-App-Development-Getting-Started/android_begin.jpg">

Hi, this blog will guide you through the basics of android app development!

## Get Started!
-----

No two apps are built in the same way, but we've structured the information you need to build an app into three sections that represent the general order for app development.

| 1. Design        |2. Develop           | 3. Distribute  |
| -------------  | ------------- | ----- |
| Before you write a single line of code, you need to design the user interface and make it fit the Android user experience. Although you may know what a user will do with your app, you should pause to focus on how a user will interact with it. Your design should be sleek, simple, powerful, and tailored to the Android experience.      | Once your design is finalized, all you need are the tools to turn your app ideas into reality. Android's framework provides you the APIs to build apps that take full advantage of device hardware, connected accessory devices, the Internet, software features, and more. With the power of Android, there's no limit to the power of your apps. | Now your app is complete. You've built it to support a variety of screen sizes and densities, and tested it on the Android emulator and on real devices. You're ready to ship your app. |

## GO!
-----

So, let's get started with downloading and installing the required software to design and develop android apps!
## Step 1 - Download [Android Studio](https://developer.android.com/studio/index.html).
- Android Studio is an IDE specially designed for Android App Development.

<img src="images/Android-App-Development-Getting-Started/android_studio.jpg">

## Step 2 - Setting up android studio.

Now that you have downloaded android studio, you are all set to install and use it. But before you get started, you have to install java on your machine. Specifically, you need to install **Java Development Kit** ([JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)) so that android studio can interpret and compile your code.
- **NOTE** - Remember the directory where you install JDK, as it will be used later.

Now, you can launch the Android Studio's installation file to proceed. Select an appropriate path for Android Studio, Android _SDK_ (A selection of tools including android platform itself) and _Android Virtual Machine_ (An emulator to test your apps on).
When you go through the installation, **make sure** you _leave the boxes ticked to confirm that you want these additional components_. You could manually add them later, but this will just complicate matters.

When you complete the installation, **don't open android studio**, close it. Create it's shortcut on your desktop and open it's properties. Then check the "**Run as administrator**" option and Apply.

Now, before moving further you need to specify the location of java to your machine. For this you create an environment variable - "**JAVA_HOME**". Here's how to do it -
1. Open **My Computer** (or, **This PC**).
2. **Right Click** (anywhere) -> **Properties**.
3. At the left hand side, you will find _**Advanced System Settings**_, click on it which will open up a dialog box.
4. In the dialog box, find and open _**Environment Variables**_ (Located under **Advanced** section).
5. Under the **User variables** section, click **New**.
6. Enter the variable name as - "**JAVA_HOME**" (without quotes) and value as the **location of your JDK**. In default case, it is - C:\Program Files\Java\jdk1.8.0_131
7. Click **OK** and **Apply** the changes and now you are ready to use android studio and make awesome apps! :smile:

When you launch Android Studio, you will be presented with a menu where you will be able to get started or configure some options. Here, you should familiarize youself with **SDK Manager** (Configure - > SDK Manager)  which is where you’ll update your Android SDK to support newer versions, as well as download things like code samples or support for Google Glass. Don’t worry about that now but if Android Studio says you’re missing something, this is where you’ll probably need to go to find it.

<img src="images/Android-App-Development-Getting-Started/android_studio_complete.png">

Now, you are all set to start building android apps! **CHEERS**! :beers:

-----
So there are mainly three things interacting when you use Android Studio to create your apps -
- Android Studio itself.
- The code you write in Java and XML.
- And the Android SDK which you’ll access through your Java code.
