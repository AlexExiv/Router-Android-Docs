# Setup

## Core modules

To start work you have to add core modules

To `Project` module add support of JitPack

```groovy
allprojects {
    repositories {
        ...
        maven { url 'https://jitpack.io' }
        ...
    }
}
```

In `App` module

```groovy
implementation "com.github.AlexExiv.Router-Android:router:$version"
implementation "com.github.AlexExiv.Router-Android:annotations:$version"
kapt "com.github.AlexExiv.Router-Android:processor:$version"
```

To add support of diffirent platforms you have to add more libs

## Platform modules

1. [Fragments](platforms/fragments/)

```groovy
implementation "com.github.AlexExiv.Router-Android:fragment:$version" // add support of fragments
```

2. [Compose](platforms/compose/)

```groovy
implementation "com.github.AlexExiv.Router-Android:compose:$version" // add support of compose
```

3. [Mixed (Fragments and Compose)](platforms/mixed.md)

```groovy
implementation "com.github.AlexExiv.Router-Android:fragment:$version"
implementation "com.github.AlexExiv.Router-Android:compose:$version"
implementation "com.github.AlexExiv.Router-Android:fragmentcompose:$version"
```

4. [Hilt Compose](injection/hilt.md)

```groovy
implementation "com.github.AlexExiv.Router-Android:compose:$version"
implementation "com.github.AlexExiv.Router-Android:android-hilt:$version"
```



