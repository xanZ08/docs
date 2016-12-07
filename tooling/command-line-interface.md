---
title: NativeScript CLI
description: Learn how to work with command line interface commands
position: 10
slug: commmand-line-interface
---

# NativeScript CLI (Command Line Interface)

The NativeScript CLI lets you create, build, and deploy NativeScript-based projects on iOS and Android devices using your terminal.

## Install the NativeScript CLI

The NativeScript CLI is available for installing as an npm package.

In the command prompt, run the following command.

OS |  Node.js installed via package manager
---|---------------------|----
Windows | `npm install nativescript -g`
OS X | `npm install nativescript -g` 
Linux | `npm install nativescript -g` 

To check if your system is configured properly, run the following command.

```
tns doctor
```

> Note: To install the nightly builds of NativeScript CLI you can use @next
> ```
> npm uninstall -g nativescript
> npm install -g nativescript@next
> ```

To see the currently installed verssion of NativeScript CLI run the following commmand.
```
tns --version
```

## Create Project

To create a new cross-platform project from the default JavaScript template, run the following command.

```
tns create MyApp
```

To create a new cross-platform project from the default TypeScript or Angular template, use the `template` option followed by either `typescript`, or `angular`.

```
tns create MyApp --template typescript
tns create MyApp --template angular
```

Or you can simply use the shorthand `tsc` and `ng` options.

```
tns create MyApp --tsc
tns create MyApp --ng
```
With the `template` option you can also specify a local or a remote path to the template that you want to use to create your project.
For example, if you want to use the nightly build of the default JavaScript template, run the following command.

```
tns create MyApp --template https://github.com/NativeScript/template-hello-world.git
```

To create a new cross-platform project from an existing NativeScript project, run the following command.

```
tns create MyApp --copy-from <Directory>
```
Where <Directory> is the complete path to the directory that contains your existing project.


## Add / Remove Platforms

After you have created your project, you can start adding target platforms to it. To be able to build your project into an application package for a selected target platform, you need to add the platform to your project first. Currently, you can target Android and iOS with your NativeScript projects.

Navigate to the directory that contains your newly created project and run the following commands.

```
tns platform add android
tns platform add ios
```

`platform add` creates the `android` and the `ios` subdirectories in the `platforms` directory. These subdirectories have the platform-specific project structure required for native development with the native SDKs for the platform.

If you need to remove platform you can run the follwing commands.
```
tns platform remove android
tns platform remove ios
```

> Note: To install the nightly builds of Android or iOS runtimes you can use @next
> ```
> tns platform add android@next
> tns platform add ios@next
> ```

## Prepare, Build, Deploy and Run Commands

Once your project is created you can proceed with the development process.
When the changes you have introduced to the project are ready for testing you will need to
build and run your application. In order to do that you have a set of avaiable commands like
`prepare`, `build`, `deploy` and `run`. Detailed explanation for each command follows below.

### Prepare

To populate the platform-specific subdirectory with the correct application assets, you need to run `prepare`.

```
tns prepare android
tns prepare ios
```

`prepare <Platform>` takes content from `app`, analyzes it and copies it to the platform-specific subdirectory in `platforms`. This operation copies common and relevant platform-specific content that applies to the selected platform. This ensures that your Android or iOS application contain only the correct assets.

Keep in mind that `prepare` overrides changes made to the platform-specific subdirectory in `platforms`. For more information, see [Development in platforms](#development-in-platforms).

### Build

After you have prepared your project, you can build it for your target mobile platforms.

```
tns build android
tns build ios
```

The NativeScript CLI calls the SDK for the selected target platform and uses it to build your app locally.

When you build for Android, the NativeScript CLI saves the application package as an `APK` in `platforms` &#8594; `android` &#8594; `bin`.

When you build for iOS, the NativeScript CLI will either build for a device, if there's a device attached, or for the native emulator if there are no devices attached. To trigger a native emulator build when a device is attached, set the `--emulator` flag.

The native emulator build is saved as an `APP` in `platforms` &#8594; `ios` &#8594; `build` &#8594; `emulator`. 

The device build is saved as an `IPA` in `platforms` &#8594; `ios` &#8594; `build` &#8594; `device`.

> **IMPORTANT:** To build your iOS app for real device, you must configure a valid certificate and provisioning profile pair, and have that pair present on your system for code signing your application package.

### Deploy

You can deploy your app on all connected devices from the selected target platform.

```
tns deploy android
tns deploy ios
```

The NativeScript CLI calls the SDK for the selected target platform and uses it to build your app locally. After the build is complete, the NativeScript CLI downloads and installs the application package on your connected devices.

On Android devices, the app runs automatically.

On iOS devices, the app does not run automatically. To run the app, tap the app icon.

> **IMPORTANT:** To deploy your app on iOS devices, you need to configure a valid pair of certificate and provisioning profile for code signing your application package.

### Run

You can quickly run your app on connected devices, including all running Android Virtual Devices. The following command is shorthand for `prepare`, `build`, and `deploy`.

```
tns run android
tns run ios
```

You can quickly deploy your app only in the native emulators using `--emulator` flag.

```
tns run android --emulator
tns run ios --emulator
```

You can test your work in progress on connected Android or iOS devices.
To verify that the NativeScript CLI recognizes your connected devices, run the following command.

```
tns device

┌───┬──────────────────┬──────────┬───────────────────┬──────────┬───────────┐
│ # │ Device Name      │ Platform │ Device Identifier │ Type     │ Status    │
│ 1 │ bullhead         │ Android  │ 00bd261c1580a7d3  │ Device   │ Connected │
│ 2 │ sdk_phone_x86_64 │ Android  │ emulator-5554     │ Emulator │ Connected │
└───┴──────────────────┴──────────┴───────────────────┴──────────┴───────────┘
```


The NativeScript CLI lists all connected physical devices and running Android Virtual Devices.
Run application on selected device using `--device <id>` flag

```
tns run android --device 2
```

Run application on selected device using `--device <Device Identifier>` flag
```
tns run android --device emulator-5554
```

Using multiple flags
```
tns run android --device emulator-5554 --log trace
```


