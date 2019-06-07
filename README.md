## 开发软件：Android Studio

### 1.Android Studio踩坑

刚安装完就遇到了这么个问题，老是让我装"Android Support Repository"，装了也给我报错。赣！

```
sync：
Unable to resolve dependency for ':app@debug/compileClasspath': Could not find any version that matches com.android.support:appcompat-v7:29.+.
Unable to resolve dependency for ':app@debugAndroidTest/compileClasspath': Could not find any version that matches com.android.support:appcompat-v7:29.+.
Unable to resolve dependency for ':app@debugUnitTest/compileClasspath': Could not find any version that matches com.android.support:appcompat-v7:29.+.
Unable to resolve dependency for ':app@release/compileClasspath': Could not find any version that matches com.android.support:appcompat-v7:29.+.
Unable to resolve dependency for ':app@releaseUnitTest/compileClasspath': Could not find any version that matches com.android.support:appcompat-v7:29.+.

Build：
Could not find any version that matches com.android.support:appcompat-v7:29.+.
Versions that do not match:
    26.0.0-alpha1
    25.3.1
    25.3.0
    25.2.0
    25.1.1
    + 50 more
Searched in the following locations:
    file:/C:/Users/oldz/AppData/Local/Android/Sdk/extras/m2repository/com/android/support/appcompat-v7/maven-metadata.xml
    file:/C:/Users/oldz/AppData/Local/Android/Sdk/extras/m2repository/com/android/support/appcompat-v7/
    file:/C:/Users/oldz/AppData/Local/Android/Sdk/extras/google/m2repository/com/android/support/appcompat-v7/maven-metadata.xml
    file:/C:/Users/oldz/AppData/Local/Android/Sdk/extras/google/m2repository/com/android/support/appcompat-v7/
    file:/C:/Users/oldz/AppData/Local/Android/Sdk/extras/android/m2repository/com/android/support/appcompat-v7/maven-metadata.xml
    https://dl.google.com/dl/android/maven2/com/android/support/appcompat-v7/maven-metadata.xml
    https://jcenter.bintray.com/com/android/support/appcompat-v7/maven-metadata.xml
    https://jcenter.bintray.com/com/android/support/appcompat-v7/
Required by:
    project :app

Please install the Android Support Repository from the Android SDK Manager.
Open Android SDK Manager
```

反正大概意思就是个版本问题，虽然不太清楚到底是哪个版本啥啥啥的，干脆直接在Module的build.gradle里这么改（改掉第三行的正则）：

```
dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'com.android.support:appcompat-v7:29.+'
    implementation 'com.android.support.constraint:constraint-layout:1.1.3'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'com.android.support.test:runner:1.0.2'
    androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.2'
}
```

```
dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'com.android.support:appcompat-v7:+'
    implementation 'com.android.support.constraint:constraint-layout:1.1.3'
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'com.android.support.test:runner:1.0.2'
    androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.2'
}
```

然后build->rebuild project

问题解决