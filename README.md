# rpg-maker-mv-player

<img src="https://img.shields.io/github/v/release/huhao1987/RMMV-android-deployment.svg">


 *The project is basic built on https://github.com/AltimitSystems/mv-android-client, although it has changed a lot of code. Thanks for Altimit Systems` code!*

#### The project is a library which help RMMV game creaters to build  _Android_  version of their games very easy.
**The project is built by kotlin, so the codes of it are less and easy to read then Java**

## How to use the library
#### Basic steps
1. You need the lastest Android studio, currently the lastest version is 3.6.2.
2. Create a new Android project or open your exist Android project.
3. After "Gradle Build Running" finish, choose the "build.gradle(Project:xxxx)", add "maven { url 'https://jitpack.io' }" in allproects
```kotlin
allprojects {
    repositories {
        google()
        jcenter()
        * maven { url 'https://jitpack.io' } *

    }
}
```

4. in "build.gradle(Module:app)", add below line in dependencies
```kotlin
implementation 'com.github.huhao1987:RMMV-android-deployment:1.0'
```

5. Now add the rpgPlayerView view in the layout of your mian activity(If you just create a new project, it should be named "MainActivity", and the name of layout should be "activity_mian")
```kotlin
 <hh.rpgmakerplayer.webviewmodule.rpgPlayerView
        android:id="@+id/rpgwebview"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />
 ```
6. In MainActivity add the lines in onCreate
```kotlin
webplayview.build()
webplayview.Playgame(path)
```
7. Build and run the debug game on your phone.

## Advance 
You can use some features in the build function of rpgPlayerview.
1) open as fullscreen or not
```kotlin
webplayview
 .isfullscreen(false/true)
 .build()
 ```
2) use your own evaluateJavascript as String
 ```kotlin
webplayview
 .setevaluateJavascript(xxxxxx)
 .build()
 ```
3) More features comming....
For example, totally fix the local mode save on Android...


## Demo
The app inside the codes are a completely app which is my own app **"rpg maker mv player"**. It is a common player which can play any RMMV game on your storage, You can play the game by chosing the index.html in the RMMV game`s folder. 


