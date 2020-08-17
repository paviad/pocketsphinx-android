About
=====

This project is a wrapper for Pocketsphinx for Android providing
high-level interface for recognizing the microphone input.

Aviad Summary
=============

1. Install Android Studio, download SDK version 28, set ANDROID_SDK_ROOT to `C:\Users\USER\AppData\Local\Android\Sdk`
2. Download swig from http://www.swig.org/download.html extract it into `C:\Local`
3. Download gradle from https://gradle.org/releases/ extract to `C:\Gradle`
4. Set GRADLE_HOME to `c:\gradle\gradle-6.6` (or the specific version number)
5. Change setvars.cmd to point to the correct swig dir (c:\local\swig-4.0.2 currently)
6. Run `setvars.cmd`
7. Run `gradle wrapper` it will install the gradle wrapper :)
8. Run `gradlew` followed by `gradlew build`

Build
=====

You will need SWIG, Gradle and Android NDK to build a distributable
archive of pocketsphinx for Android. It is better to use recent versions.

You need to checkout sphinxbase, pocketsphinx and pocketsphinx-android
and put them in the same folder.

```
Root folder
 \_pocketsphinx
 \_sphinxbase
 \_pocketsphinx-android
```

Older versions might be incompatible with the latest pocketsphinx-android,
so you need to make sure you are using latest versions. You can use
the following command to checkout from repository:

```
git clone https://github.com/cmusphinx/sphinxbase
git clone https://github.com/cmusphinx/pocketsphinx
git clone https://github.com/cmusphinx/pocketsphinx-android
export POCKETSPHINX_HOME=`pwd`/pocketsphinx
export SPINXBASE_HOME=`pwd`/sphinxbase
```

After checkout you need to update the file 'local.properties' in the
project root and define the following properties:

  * sdk.dir - path to Android SDK
  * ndk.dir - path to Android NDK

For example:

```
sdk.dir=/Users/User/Library/Android/sdk
ndk.dir=/Users/User/Library/Android/sdk/ndk-bundle
```

After everything is set, run `./gradlew build`. It will create
pocketsphinx-android-5prealpha-release.aar and
pocketsphinx-android-5prealpha-debug.aar in build/output.

Using the library
=================

Add bintray maven to your repositories

    allprojects {
        repositories {
            maven {
                url  "https://dl.bintray.com"
            }
            jcenter()
            google()
        }
    }


Add `pocketsphinx-android` to your dependencies

    dependencies {
        implementation 'edu.cmu.pocketsphinx.android:pocketsphinx-android:5prealpha@aar'
    }


Using the library locally
=================

Library is distributed as android archive AAR. You can add it to your project
as usual with Android Studio or directly in gradle

    dependencies {
        compile (name:'pocketsphinx-android-debug', ext:'aar')
    }

    repositories {
        flatDir {
                dirs 'libs'
        }
    }

For further information on usage please see the wiki page:

http://cmusphinx.sourceforge.net/wiki/tutorialandroid
