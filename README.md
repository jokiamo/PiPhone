# PiPhone

[![Version](https://img.shields.io/cocoapods/v/CustomBrowserKit.svg?style=flat)](http://cocoapods.org/pods/PiPhone)
[![License](https://img.shields.io/cocoapods/l/CustomBrowserKit.svg?style=flat)](http://cocoapods.org/pods/PiPhone)
[![Platform](https://img.shields.io/cocoapods/p/CustomBrowserKit.svg?style=flat)](http://cocoapods.org/pods/PiPhone)

PiPhone is a framework that drops in picture-in-picture support (user-initiated playback of video in a floating, resizable window) for iPhone devices. It's designed to mimic default `AVPictureInPictureController` behavior as much as possible.

## Overview

<p align="center">
<img width="281" height="500" src="https://github.com/ky1vstar/PiPhone/blob/master/Demonstration/PiPhone.gif?raw=true">
</p>

## Features
- [x] Picture in picture support for devices that doesn't support it by default
- [x] No additional work required if `AVPictureInPictureController` have been already configured
- [x] Same appearance as default one
- [x] Handling video size changing
- [x] Handling video errors
- [x] Supports tap, double tap, pinch and pan gestures
- [x] Mimic `AVPictureInPictureControllerDelegate` behavior

## Requirements

* Xcode 8.0+
* iOS 9.0+

## Installation

PiPhone is available through [CocoaPods](http://cocoapods.org). To install it, simply add the following line to your Podfile:

```ruby
pod 'PiPhone'
```

## Usage

To display video in picture-in-picture mode you can use both `AVPlayerViewController` and any custom video player [configured to be diplayed in picture-in-picture](https://developer.apple.com/documentation/avkit/adopting_picture_in_picture_in_a_custom_player "configured to be diplayed in picture-in-picture").

Basically you don't need to perform any additional actions, your video players support picture-in-picture now! But `PiPhone` provides some customizations that you can find useful.

Make sure to import the framework header: `#import <PiPhone/PiPhone.h>` for Objective-C or `import PiPhone` for Swift.

### Content inset adjustment behavior

Default `AVPictureInPictureController` behavior is to find the topmost `UINavigationController`'s bar, `UITabBarController`'s bar, `safeAreaInsets`, etc and determine where to place overlay video based on this metrics. Since imitation of this behavior turned out to be complicated and tricky process, it've been decided to control overlay video position based on predefined configurations.

**PiPManagerContentInsetAdjustmentNavigationBar**
Includes safe area insets and additional 44dp (32dp on landscape) inset from top safe area.

**PiPManagerContentInsetAdjustmentTabBar**
Includes safe area insets and additional 49dp (32dp on landscape in iOS 11 and above) inset from bottom safe area.

**PiPManagerContentInsetAdjustmentNavigationAndTabBars**
Includes both `PiPManagerContentInsetAdjustmentNavigationBar` and `PiPManagerContentInsetAdjustmentTabBar`.

**PiPManagerContentInsetAdjustmentSafeArea**
Includes safe area insets.

**PiPManagerContentInsetAdjustmentNone**
Overlay video is pinned to screen edges.

This behavior can be changed via `PiPManager`'s `contentInsetAdjustmentBehavior` property.

**Objective-C**
```objectivec
PiPManager.contentInsetAdjustmentBehavior = PiPManagerContentInsetAdjustmentNavigationAndTabBars;

// animated
[UIView animateWithDuration:0.25 animations:^{
PiPManager.contentInsetAdjustmentBehavior = PiPManagerContentInsetAdjustmentNavigationAndTabBars;
}];
```

**Swift**
```swift
PiPManager.contentInsetAdjustmentBehavior = .navigationAndTabBars

// animated
UIView.animate(withDuration: 0.25) {
PiPManager.contentInsetAdjustmentBehavior = .navigationAndTabBars
}
```

### Additional content insets

Also you can set extra spacing from screen edges to overlay video which will be added to automatically calculated one.

**Objective-C**
```objectivec
PiPManager.additionalContentInsets = UIEdgeInsetsMake(20, 10, 20, 10);

// animated
[UIView animateWithDuration:0.25 animations:^{
PiPManager.additionalContentInsets = UIEdgeInsetsMake(20, 10, 20, 10);
}];
```

**Swift**
```swift
PiPManager.additionalContentInsets.top = 20

// animated
UIView.animate(withDuration: 0.25) {
PiPManager.additionalContentInsets.top = 20
}
```

### Disable picture-in-picture

You can temporarily disable picture-in-picture mode causing `AVPictureInPictureController`'s `isPictureInPicturePossible` property to be `false`.

**Objective-C**
```objectivec
// enable
PiPManager.pictureInPicturePossible = YES;

// disable
PiPManager.pictureInPicturePossible = NO;
```

**Swift**
```swift
// enable
PiPManager.isPictureInPicturePossible = true

// disable
PiPManager.isPictureInPicturePossible = false
```

## Example

To run the example project, clone the repo, and run `pod install` from the Example directory first.

## License

CustomBrowserKit is available under the MIT license. See the LICENSE file for more info.

