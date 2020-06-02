# Android Versioning Gradle Plugin

This plugin automatically generates your Android versionName and versionCode using Git. It also appends the version and variant names to your ABB/APK artifacts.

## Usage

### `buildscript` block:
```groovy
// top-level build.gradle
buildscript {
  repositories {
    jcenter()
  }
  dependencies {
    classpath 'eu.nanogiants:android-versioning:2.0.0'
  }
}
```
```groovy
// app build.gradle
apply plugin: 'eu.nanogiants.android-versioning'
```

or via the (if you also apply the `com.android.application` this way)

### `plugins` block:
```groovy
plugins {
  id 'com.android.application'
//...
  id 'eu.nanogiants.android-versioning' version '2.0.0'
}
```

### Version code and name
```groovy
android {
  defaultConfig {
    versionCode versioning.getVersionCode()
    versionName versioning.getVersionName()
  }
}
```
**Use the plugin by referencing the versioning extension.**

* `getVersionCode()` returns the current Git commit count
* `getVersionName()` returns the latest Git tag of your repository

#### Optional:
* `getVersionName(checkBranch: Boolean)` if `checkBranch` is set to *true* the plugin will check if the current branch is `release/x.x.x` or `hotfix/x.x.x` and use the naming instead the latest tag.

### Artifact naming

The plugin will automatically set the APK and AAB naming for all assemble and bundle tasks. This will also work if you do not use the versioning extension in the defaultConfig. You can still use the default `archivesBaseName` property.

#### Example:

Build Variant `productionStoreDebug`
```groovy
android {
  defaultConfig {
    archivesBaseName = "MyAppName"
  }
}
```
Artifacts:
```
MyAppName-production-store-3.9.0-3272-debug.apk
MyAppName-production-store-3.9.0-3272-debug.aab
```
#### Optional:
You can define a comma separated list of buildTypes (e.g. debug) be excluded from the artifact naming.
```groovy
versioning {
  excludeBuildTypes = "debug" {
}
```

## License
	Copyright (C) 2020 NanoGiants GmbH

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
