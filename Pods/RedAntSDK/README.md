# RedAntSDK

SDK is the set of tools that allows you to create your own application with benefits and specials of SS VPN  or integrate it into your existing application.
# Setup
# Normal
Drag and drop RedAnt.framework, ShadowPath.framework  into your project. 

In order to use it you have to add -ObjC linker flag in XCode (Target > Build Settings > Linker > Other Linker Flags). You also have to add the following additional frameworks and libraries to XCode (Target > Build Phases > Link Binary With Libraries):

* KissXML.framework
* CocoaAsyncSocket.framework
# Cocoapod
```sh
pod 'RedAntSDK', :git => 'git:https://github.com/toffs-dev/M88-SSClient-iOS-SDK.git'
```

After the setup is completed, you should be able to use all the classes from the SDK by including it with the #import <RedAntManager/RedAntManager.h> directive.

* Add appgroup info  in your plist file (main project - extension )
```sh
    RedAntAppGroup : "your.app.group.name"
```

* Add network extension to your existing app  and subclass RedAntPacketTunnelProvider

* Implement this function in Appdelegate.m
```sh
 RedAntManager.setup(bundleGroupID: "group.demo.vn.demo") //required, your appgroup name
```
* To handle status of VPN you can subscribe 
```sh
    kProxyServiceVPNStatusNotification
```
* Start, stop VPN 
```sh
RedAntManager.sharedManager.startVPN()
RedAntManager.sharedManager.stopVPN()
```
# Note:
The current version of the RedAnt SDK uses the following libraries under the hood:

* libcurl
* libssl
* libcares
* libcrypto

If your project uses one of these libraries and you get conflicts, please contact the RedAnt team or create git issues  for further investigation.

## To debug the VpnExtension process

* VpnExtension runs in a separate process and its output is not logged to the Xcode console. To view its log statements, open the Console.app and filter messages that contain "Outline" or “VpnExtension”.
* In XCode, click top Debug menu → Attach to Process → VpnExtension
* This can only be done once the VPN Extension is running (after you are connected).
* [Detailed instructions](https://developer.apple.com/library/content/documentation/General/Conceptual/ExtensibilityPG/ExtensionCreation.html#//apple_ref/doc/uid/TP40014214-CH5-SW8).

#  Prerequisites to build
* You need an iPhone. Network Extension App cannot run in iOS Simulators, you need a real iPhone to debug.


# Xcode 7.x+ and App Transport Security
The  SDK uses a local HTTP server to download VPN profiles (which does not use the NEVPNManager class). You must include the Allow Arbitrary Loads flag in your project's Info.plist file if you use Xcode 7.x+. See Apple's documentation regarding this issue.

# Network Extension
Supported protocols:
* ShadowSock server

# Class
- RedAntManager.swfit
- RedAntPacketTunnelProvider.h

# Changes log 

Version 1.0 : 
- First release.
