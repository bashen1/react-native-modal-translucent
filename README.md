# react-native-modal-translucent

Remove the StatusBar background for Modal on Android

### Before

<img src="./screenshot/before.jpg" width=300>

### After

<img src="./screenshot/after.png" width=300>

### Usage

#### First Install

```bash
npm install react-native-modal-translucent --save
```

**or**

```bash
yarn add react-native-modal-translucent
```

#### Last Link

```javascript
$ react-native link react-native-modal-translucent
```

That is All !

Now go to see the effect.

## Caveat

If your react-native version is below 0.57, you need to update your android gradle.

First, modify your android/build.gradle

```diff
buildscript {
+    ext {
+        buildToolsVersion = "27.0.3"
+        minSdkVersion = 16
+        compileSdkVersion = 27
+        targetSdkVersion = 26
+        supportLibVersion = "27.1.1"
+    }

    repositories {
+        google()
         jcenter()
-        maven {
-            url 'https://maven.google.com/'
-            name 'Google'
-        }
    }

    dependencies {
-        classpath 'com.android.tools.build:gradle:2.3.3'
+        // make sure your gardle version here is equal or greater than 3.1.4
+        classpath 'com.android.tools.build:gradle:3.1.4'
    }
}

allprojects {
    repositories {
         mavenLocal()
+        google()
         jcenter()
         maven {
             url "$rootDir/../node_modules/react-native/android"
         }
-        maven {
-            url 'https://maven.google.com/'
-            name 'Google'
-        }
    }
}

-ext {
-    buildToolsVersion = "26.0.3"
-    minSdkVersion = 16
-    compileSdkVersion = 26
-    targetSdkVersion = 26
-    supportLibVersion = "26.1.0"
-}


+task wrapper(type: Wrapper) {
+    gradleVersion = '4.4'
+    distributionUrl = distributionUrl.replace("bin", "all")
+}
```

Second, modify android/gradle/wrapper.gradle-wrapper.properties, make sure the gradle distribution is equal or greater than 4.4

```diff
distributionBase=GRADLE_USER_HOME
distributionPath=wrapper/dists
zipStoreBase=GRADLE_USER_HOME
zipStorePath=wrapper/dists
-distributionUrl=https\://services.gradle.org/distributions/gradle-3.5.1-all.zip
+distributionUrl=https\://services.gradle.org/distributions/gradle-4.4-all.zip
```
