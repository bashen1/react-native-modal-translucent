# react-native-modal-translucent

Remove the StatusBar background for Modal on Android

### Before

<img src="./screenshot/before.jpg" width=320>

### After

<img src="./screenshot/after.png" width=320>

### Usage

#### First

| React Native version(s) | Supporting version(s) |
| ----------------------- | --------------------- |
| >= 0.60                 | 4.0.1                 |
| < 0.60                  | 3.0.2                 |


```bash
npm install react-native-modal-translucent --save
# or
yarn add react-native-modal-translucent
```

#### Second

```javascript
$ react-native link react-native-modal-translucent
```

#### Finally

Modify package.json

```diff
 "scripts": {
    "start": "node node_modules/react-native/local-cli/cli.js start",
    "test": "jest",
+   "fix-modal": "node node_modules/react-native-modal-translucent/scripts/translucent-modal.js",
+   "postinstall": "npm run fix-modal"
 }
```

Run fix-modal once

```bash
npm run fix-modal
```

That is All !

Now run the app and see the effect.

## Caveat

If your react-native version is below 0.57, you need to update your android gradle.

First, modify your android/build.gradle

```diff
buildscript {
+    ext {
+        buildToolsVersion = "28.0.3"
+        minSdkVersion = 16
+        compileSdkVersion = 28
+        targetSdkVersion = 28
+        supportLibVersion = "28.0.0"
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
+        // make sure your gardle version here is equal or greater than 3.3.2
+        classpath 'com.android.tools.build:gradle:3.3.2'
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
+    gradleVersion = '4.10.1'
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
+distributionUrl=https\://services.gradle.org/distributions/gradle-4.10.1-all.zip
```
