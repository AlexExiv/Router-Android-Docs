# Overview

Provides an easy solution for screen navigation in the Android, eliminating the need to understand the Fragment lifecycle or implement transitions in Compose. Also, supports mixed transitions between [Fragments](platforms/fragments/) and [Compose](platforms/compose/) screens if you are [migrating](platforms/mixed.md) from the Fragments to Compose or have [mixed](platforms/mixed.md) project at all.&#x20;

[Framework GitHub Repository](https://github.com/AlexExiv/Router-Android/tree/main)

{% embed url="https://github.com/AlexExiv/Router-Android/tree/main" %}
Framework GitHub Repository
{% endembed %}

Latest release verion:

[![](https://jitpack.io/v/AlexExiv/Router-Android.svg)](https://jitpack.io/#AlexExiv/Router-Android)

## Goals

1. Project decoupling. Keep the business logic separate from the navigation logic, maintaining a clean architecture.
2. Easy navigation between screen
3. Send parameters to the screen you want to navigate to and get a result from its job
4. Intercept navigation and replace it by a new one if needed. For example signin screen for unathorized users
5. Opportunity to close a sequence of screens united in a group. For example you have wizard with several steps and you need to close it all once a user completes his journey
6. Deep links
7. Happy life

## Philosophy

The main idea of Router is to avoid navigation calls like these:

```kotlin
// show new fragment in the parent Fragment
parentFragment?.showFragment(NewFragment.newInstance())

// show dialog
showDialog(NewDialogFragment.newInstance())

// or change tab
(parentFragment as TabsFragment).changeTab(0)

// or another way to change tab
App.shared.mainActivity.changeTab(0)

//or whatever it is
```

By doing so, you add extra dependencies between screens. Instead, navigation should be handled in a way that the screen only knows it needs to navigate, but not the specifics of how that navigation is performed. This keeps the business logic separate from the navigation logic, maintaining a clean architecture.

You should only call `router.route(ScreenPath())`, and the router will handle displaying the screen as it should be shown. It will change the selected tab, close to the screen if it exists in the stack, or present it in full screen.

## Features

1. [Navigation](navigation/) between screens
2. [Transfer result](result-api.md) between screens
3. [Middleware](middleware.md) intercepts navigation between screens, blocking it or replacing it with another navigation
4. [Chain](chains.md) - united sequence of screens
