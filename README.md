# iOS Cheatsheet
Here's a list of things and commands that I use commonly when working in iOS.

### Carthage commands
Install
```sh
brew update
brew install carthage
```
Add libraries to a file called Cartfile like this
```sh
github "Alamofire/Alamofire" ~> 4.3
```
Then run
```sh
carthage update --platform iOS
```
To update a single entry put the name of the library written equal to Cartfile, if that doesn't work put the last part of the library's github url.
```sh
carthage update LibraryName --platform iOS
```
If using SwiftJSON and having an error
```sh
carthage update --platform iOS --no-use-binaries
```
When you have the .framework files add them to the project by dragging and dropping them. Then go to Project settings -> Build phases tab, click the "+" buton and add a "Copy Files" phase. In this section set the field "Destinations" to "Frameworks" if not set.

When uploading a project to the app store and having problems of "library not found"
On your application targets’ “Build Phases” settings tab, click the “+” icon and choose “New Run Script Phase”. Create a Run Script in which you specify your shell (ex: bin/sh), add the following contents to the script area below the shell:
```sh
/usr/local/bin/carthage copy-frameworks
```
and add the paths to the frameworks you want to use under “Input Files”, e.g.:
```sh
$(SRCROOT)/Carthage/Build/iOS/Box.framework $(SRCROOT)/Carthage/Build/iOS/Result.framework
$(SRCROOT)/Carthage/Build/iOS/ReactiveCocoa.framework
```
This script works around an App Store submission bug triggered by universal binaries and ensures that necessary bitcode-related files and dSYMs are copied when archiving.

## Git
Configure a .gitgnore going to [gitignore.io](https://www.gitignore.io) and writing Xcode and Swift.
