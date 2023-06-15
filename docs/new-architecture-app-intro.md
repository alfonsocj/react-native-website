---
id: new-architecture-app-intro
title: Prerequisites for Applications
---

import NewArchitectureWarning from './\_markdown-new-architecture-warning.mdx';
import Tabs from '@theme/Tabs'; import TabItem from '@theme/TabItem';
import constants from '@site/core/TabsConstants';

<NewArchitectureWarning/>

There are a few prerequisites that should be addressed before the New Architecture is enabled in your application.

## Update to the latest React Native version

React Native released the support for the New Architecture with the release `0.68.0`.

This guide is written with the expectation that you’re using the [**latest** React Native release](https://github.com/facebook/react-native/releases/latest).

You can find instructions on how to upgrade in the page [upgrading to new versions](/docs/upgrading).

Remember to run `yarn` after upgrading.

:::important

Whenever you have to rename some files in the `ios` folder, please **use Xcode to rename them**. This ensure that the file references are updated in the Xcode project as well. You might need to clean the build folder (_Project → Clean Build Folder_ or `⌘ + ⇪ + k`) before re-building the app. If the file is renamed outside of Xcode, you may need to click on the old `.m` file reference and Locate the new file.

:::

## Android - Enable the New Architecture

If you successfully updated your project to the latest version of React Native, you **already meet** all the prerequisites to use the New Architecture on Android.

You will only need to update your `android/gradle.properties` file as follows:

```diff
# Use this property to enable support to the new architecture.
# This will allow you to use TurboModules and the Fabric render in
# your application. You should enable this flag either if you want
# to write custom TurboModules/Fabric components OR use libraries that
# are providing them.
-newArchEnabled=false
+newArchEnabled=true
```

## iOS - Enable the New Architecture

If you successfully updated your project to the latest version of React Native, you **already meet** all the prerequisites to use the New Architecture on iOS.

You will only need to reinstall your pods by runningpod install with the right flag:

```bash
// Run pod install with the flags
RCT_NEW_ARCH_ENABLED=1 bundle exec pod install
```

## Running the App

It’s now time to run your app to verify that everything works correctly:

```bash
# To run android
yarn android

# To run iOS
yarn ios
```

In your Metro terminal log, you will now see the following log to confirm that Fabric is running correctly:

```
BUNDLE ./App.tsx
LOG Running "App" with {"fabric":true,"initialProps":{"concurrentRoot": "true"},"rootTag":1}
```

## Advanced - Pass your component in the interop layer

If you followed the previous steps but your app uses some custom Native Components that have not been migrated to the New Architecture completely, you are going to see some reddish/pinkish boxes saying that the component is not compatible with Fabric. This is happening because custom Native Components written for the legacy architecture can't run as-is in the New Architecture.

Starting from React Native 0.72, we worked on a interoperability layer to let you use legacy components in the New Architecture without having to wait for them to be migrated.

<!-- TODO: Add link to the WG as soon as we publish it. -->

You can read more about the interoperability layer and how to use it [here](). Follow this guide to register your components and then rerun your app with the commands:

```bash
# To run android
yarn android

# To run iOS
yarn ios
```
