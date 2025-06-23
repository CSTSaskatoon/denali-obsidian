# Cross Platform Tools
- Allows writing code once which is used to create apps for each platform.
- Often each platform has quirks which complicates things

## Types
### Native Compilation
- Tools that let you compile code on multiple platforms
- App produced will be "native" for each individual platform

#### Examples
- **Xamarin** (C# based)
- **Maui** (C# based)

### Hybrid Apps
- Usually for mobile
- Web view wrapped in a native app
- Native app just displays web view control
- web view control shows web interface, runs via the browser
- Often the web view can access some device features such as contacts, gps, battery etc. through the native app
- Also includes **Interpreted language** apps, although they aren't common

#### Examples
- **Cordova**/**Phonegap** - open source, free cloud build service
- **Ionic Framework** - originally built on Cordova but now built on **Angular**
- **Intel XDK** - built on Phonegap
- **React Native** - made by Facebook
- **Flutter** - made by Google

## Advantages
- Learn one tool, deploy to multiple platforms
- If the tool is robust and up to date you don't need to learn new platforms
- Fast prototyping of simple apps, templates

## Disadvantages
- The tools often change so you have to keep up
- Lowest common denominator, often missing features or quirks in one platform will impact all other platforms in order to keep the functionality the same
- Debugging sucks on these
- Might be best to create custom apps on target platforms instead, though now you need expertise in multiple platforms and update all of them around the same time

## Hybrid Apps
### History
- Cordova made by *Nitobi*, bought by *Adobe* in 2011
- Adobe released open source version called **Apache Cordova** later
- Cordova supports to some extent Android, Windows Phone, iOS, Blackberry, Ubuntu, Firefox OS, Fire OS, Windows Desktop

### How they work
- Not truly native or completely web based
- Layout rendering done by web views, wrapped as applications
- Have access to device APIs through libraries and plugins

#### Online Build Service
- `Build.phonegap.com`
- Allows building for Windows 8, Android and iOS (if you have a dev license)
- Other platforms have to be built on the command line

#### Plugins
- Found online
- Support is not always complete for all platforms
- Android and iOS are most widely supported

## Native Apps (Xamarin)
### History
- Made by team that created **Mono** (`.NET` framework port)
- Originally had a separate IDE called *Xamarin Studio* which is deprecated
- **`Xamarin.Mac`** allowed building C# apps for OS X in 2012
- **Xamarin 3** - **`Xamarin.Forms`** allows "portable controls" which are mapped to the native controls of each platform
- Microsoft acquired Xamarin in 2016 and released the toolset for free, switched to Visual Studio as the main IDE for it

### Projects in Xamarin
- Solution is generated with multiple projects in it
	- **Shared Project** - Majority of code, isn't platform specific
	- **iOS Project** - iOS specific code for accessing device features and dealing with quirks of iOS
	- **Android Project** - same as iOS but for Android
	- **Windows UAP Project** - not used by us, don't worry about it
- Use a USB to connect a device, or an Emulator and the Android SDK to debug on Android
- Use a "remote agent" on Mac to Debug on iOS

### Output Platforms
- Outputting and building for Android works well and uses the Android SDK tools
	- Visual Studio handles images, API levels, etc.
	- APK is packaged and deployed on device, or deployed on the store
- Development for iOS is done on Windows, **compiling and deployment is done on a remote Mac system**
	- Xamarin Agent and Local User on Mac must have local admin
	- Requires current version of **XCode** and **Xamarin Mac** software
	- Log in user on Mac, connect to the session from Visual Studio
	- Remote Agent can deploy to iOS simulator which is visible on the Mac
