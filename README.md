# Overview

Provides an easy solution for screen navigation in the Android, eliminating the need to understand the Fragment lifecycle or implement transitions in Compose. Also, supports mixed transitions between [Fragments](platforms/fragments.md) and [Compose](platforms/compose.md) screens if you are [migrating](platforms/mixed.md) from the Fragments to Compose or have [mixed](platforms/mixed.md) project at all.&#x20;

## Goals

1. Easy navigation between screen
2. Send parameters to the screen you want to navigate to and get a result from its job
3. Intercept navigation and replace it by a new one if needed. For example signin screen for unathorized users
4. Opportunity to close a sequence of screens united in a group. For example you have wizard with several steps and you need to close it all once a user completes his journey
5. Deep links
6. Project decoupling
7. Happy life

## Features

1. [Navigation](navigation/) between screens
2. Transfer result between screens
3. [Middleware](middleware.md) intercepts navigation between screens, blocking it or replacing it with another navigation
4. [Chain](chains.md) - united sequence of screens
