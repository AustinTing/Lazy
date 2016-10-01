Gradle
====
top apply plugin:
```
//      Butter Knife
apply plugin: 'android-apt'
```
dependencies:
```
//    firebase-ralated and play-services-auth must are the same !
compile 'com.google.firebase:firebase-auth:9.6.1'
compile 'com.google.firebase:firebase-database:9.6.1'
compile 'com.google.android.gms:play-services-auth:9.6.1'
//    Butter knife
compile 'com.jakewharton:butterknife:8.4.0'
apt 'com.jakewharton:butterknife-compiler:8.4.0'
//    Percent Layout
compile 'com.android.support:percent:24.2.1'
```
bottom apply plugin:
```
apply plugin: 'com.google.gms.google-services'
```

