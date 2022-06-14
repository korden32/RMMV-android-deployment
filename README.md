# RMMV-android-deployment

<img src="https://img.shields.io/github/v/release/huhao1987/RMMV-android-deployment.svg">

## [点击阅读中文文档](https://github.com/huhao1987/RMMV-android-deployment/blob/master/README.zh_CN.md "简体中文")	


 *The project is built on https://github.com/AltimitSystems/mv-android-client, although it has changed a lot of code. Thanks for Altimit Systems` code!*

#### The project is a library which helps RMMV game creators to build  _Android_  version of their games very easy.
**The project is built by kotlin, so the codes of it are less and easier to read than Java**

## Update Log ##
**Add Save type support**

**Add Android internal storage save support(with my RMMV plugin)**

**Add custom save path setup**

## How to use the library
#### Basic steps
- You need the latest Android studio, currently, the latest version is 2021.2.1.
- Create a new Android project with "empty activity" or open your exist Android project, wait for "Gradle Build Running" finish.
- Gradle Scripts > `settings.gradle`, add into `dependencyResolutionManagement > repositories`:
```kotlin
maven { url 'https://jitpack.io' }
```
- Gradle Scripts > `build.gradle(Module:XXXX.app)`, add into `dependencies`:
```kotlin
implementation 'com.github.huhao1987:RMMV-android-deployment:1.0.9'
```
- Manifests > `AndroidManifest.xml`, add into `activity` tag:
```kotlin
       android:configChanges="orientation|screenSize"
       android:screenOrientation="sensorLandscape"
```
to make the game run as horizontal screen

* If your game need network connection

5.1 please add 
```kotlin
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```
5.2 in "application" tag, add 
```kotlin
        android:networkSecurityConfig="@xml/network_security_config"
```
5.3 right click "app"->"New"->"Android Resource Directory",  then choose "xml" in Resource type.
    right click "xml"->"New"->"XML Resource file",name it as "network_security_config", and copy the code below inside
```kotlin
<?xml version="1.0" encoding="utf-8"?>
<network-security-config>
    <base-config cleartextTrafficPermitted="true" />
</network-security-config>
```
5.1 and 5.2 are used to give the network permission for your game, or it cannot connect to the Internet. 5.2 ensure that the app can connect to both "http" and "https"


- Now add the rpgPlayerView view in the layout of your main activity (If you just create a new project, it should be named "MainActivity", and the name of layout should be "activity_main")
```kotlin
 <hh.rpgmakerplayer.webviewmodule.rpgPlayerView
        android:id="@+id/rpgwebview"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
 ```
 
- If your project doesn`t have assets folder, right click "app"-"New"->"Folder"->"Assets Folder",Put the folder "www" of RMMV game in to "assets" folder.

- In MainActivity add the lines
- - in import:
```kotlin
import hh.rpgmakerplayer.webviewmodule.rpgPlayerView;
```
- - in onCreate
* kotlin:
```kotlin
rpgwebview.build()
rpgwebview.Playgame("//android_asset/www/index.html")
```
* Java:
```Java
rpgPlayerView rpgwebview=findViewById(R.id.rpgwebview);
rpgwebview.build();
rpgwebview.Playgame("//android_asset/www/index.html",false);
```

9. Build and run the debug game on your phone.

## Advance 
You can use some features in the build function of rpgPlayerview.
1) open as fullscreen or not
```kotlin
rpgwebview
 .isfullscreen(false/true)
 .build()
 ```
2) use your own evaluateJavascript as String
 ```kotlin
rpgwebview
 .setevaluateJavascript(xxxxxx)
 .build()
 ```
 
3) **Android save support**

   As the limitation of Android system, the RMMV cannot store the save in the internal storage. I wrote a RMMV plugin to support it.
   It`s easy to use, just use my deployment method above to create your Android game project, and Add the "hh_Android_save.js" from [here](https://github.com/huhao1987/RMMV-Plugins), and add it in your RMMV game project and turn on it.
   
 4) **custom save path setup**
 
    Add custom save path setup function which allows you to storage the save locally, but you need to add the write storage permission firstly.
     
 ```kotlin
rpgwebview.setupcustompath("your path")
rpgwebview.build()
   ```
   **Remember to update the assets folder in your android project after modification**
   
   After these stages, when you test and play the game, the game saves will be saved in the internal storage, right now the path will be in the root folder, you could only find out them if you rooted your phone.
    
5) More features comming....


