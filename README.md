# iOS Cheatsheet
Here's a list of things and commands that I use commonly when working in iOS.

## 👍 Good practices
Must read https://github.com/futurice/ios-good-practices

## 🛠 Carthage commands
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

## 📮 Git

### Alias
Go to your home folder and edit the .gitconfig file (if it doesn't exist create it). Add this:
```sh
[alias]
        ci = commit
        st = status -sb
        co = checkout
        b = branch
        merf = merge --no-ff
        ls = ls-files
        type = cat-file -t
        dump = cat-file -p
        viff = difftool -y -t vimdiff
        gl = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-comm$
        dlog = log --oneline --decorate
[merge]
        tool = vimdiff
        keepBackup = false
```
### Gitflow commands
git co -b devNewBranch
(Do all the work you want)
git co develop
git fetch origin
git rebase -pk origin/develop
git merf devNewBranch
(solve conflicts)
git push origin develop
### iTerm2
Go to https://www.iterm2.com and download the app. This is your new terminal forever.
### OhMyZsh
Go to OhMyZsh and install it https://github.com/robbyrussell/oh-my-zsh. Now you have iTerm2 + OhMyZsh. Apply the git plugin at least as explained in the web. Then go to preferences in iTerm2 and go to Profiles -> Defaut -> Colors -> Colors Presets... and choose "Solarized Dark", I recomend you change some colors for the Solarized Light to have a fancier terminal like this:

<p align="center">
<img src="https://raw.githubusercontent.com/xavipedrals/iosCheatSheet/master/Screen%20Shot%202017-04-07%20at%2013.18.04.png" width="60%" margin="auto">
</p>

### Use Sublime text from the terminal
Although I generally use nano when editing text files from the terminal it might fall short sometimes, you can run Sublime Text from the termial after creating a symbolic link to a directory that is part of your $PATH.
We are going to use /usr/local/bin/ so first do
```sh
echo $PATH
```
... and ensure that /usr/local/bin/ is part of it. Then ensure you can run sublime from the terminal using it's full path, try to run:
```sh
/Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl
```
If it's successful it's time to create a symbolic link to /usr/local/bin/, run:
```sh
sudo ln -s /Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl /usr/local/bin/subl
```
Now you should be able to run Sublime from the terminal by typing
```sh
subl
```
### Gitignore
Configure a .gitgnore going to [gitignore.io](https://www.gitignore.io) and writing Xcode and Swift.

## 🎏 Rx Swift (Reactive Programming)
Here you can find RxSwift and some examples https://github.com/ReactiveX/RxSwift.
For when default Rx table/collectionViews falls short https://github.com/RxSwiftCommunity/RxDataSources.
### 🎈 RxMarbles
This let's you see in a super easy graphic way the manipulations you can do to an observable. I use it a lot.
http://rxmarbles.com

## 📷 iOS Assets (generate @3x, @2x)
To generate the image assets here you have an automator service that will be the best thing to generate @2x and @1x images from @3x images.
http://kristian.co/2014/10/07/a-workflow-for-scaling-retina-assets.html
If you need to add @3x suffix to images names you can select multiple images and do a multiple rename.

## ✒️ iOS App Icon 
The following automator script let's you select a 1024x1024 image and generates all the assets that Apple asks you for your app icon.

[Download automator file](https://github.com/xavipedrals/iosCheatSheet/raw/master/App%20asset%20generator.zip)
<p align="center">
<img src="https://raw.githubusercontent.com/xavipedrals/iosCheatSheet/master/automator.jpg" width="20%" margin="auto">
</p>


## 🗓 Struggling with Date
Here you have the most useful web for playing with Date formats in Swift
http://nsdateformatter.com

## 📏 iOS icon sizes
If you doubt about the icon sizes in a iOS app here you have the matrix you are looking for:
https://developer.apple.com/ios/human-interface-guidelines/graphics/custom-icons/

## 📫 Push notifications
To test your push notifications you can use this app, Pusher, easy installed via Homebrew:
https://github.com/noodlewerk/NWPusher

## ✂️ Trouble with autolayout
If you have completely unreadable layout errors just paste them here:
https://www.wtfautolayout.com

## 🔬 Working with Xcode beta
You can have the stable version and the beta version of Xcode installed withou problem. The thing you must take into account is the compiler. Probably the ncompiler will have different versions of Swift and this can be a problem especially when using external libraries. To correct this problem you can run:

```sh
sudo xcode-select --switch /Applications/Xcode-beta.app/Contents/Developer
```

Then to update the libraries and compile them in the latest version of Swift you can run:
```sh
carthage update --platform iOS --no-use-binaries
```

To revert and use the stable version of Xcode you will need to recompile you libraries, before that be sure to run:

```sh
sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
```

## 🔨 Debbuging tips and tricks
### 👀 po
Most basic command you need to know for the debugger is 
```sh
po variable
```
Which will print the contents of a variable.
### 💪 expression
Here is where it starts to get interesting, `expresion` allows you to execute a line of code in real time without recompiling the app, for example:
```sh
expresion isFinished = true
```
Would change the value of a variable. You can also do things like:
```sh
expresion object.doWork()
```
Which will run the function on run-time.
### ☎️ HTTPS debugging
If you have certificate pinning enabled and Charles is tricky to use try to add this library to your project https://github.com/pmusolino/Wormholy. It displays all the http requests made by a device by shaking it.

### ⏸ Breakpoints
Breakpoints have more options than the majority of developers know, doble click a breakpoint and then an options panel as the one in the screenshot appears:

<p align="center">
<img src="https://raw.githubusercontent.com/xavipedrals/iosCheatSheet/master/breakpoint-options.png" width="60%" margin="auto">
</p>

Here you can make your breakpoint conditional but the most interesting part is that your breakpoint can evaluate multiple debugger commands, like printing an object and changing a variable, like in the screenshot. Also the checkbox `Automatically continue` allows your execution to continue without stopping, this way you can inject code into the app for debugging purposes.
### 🈺 Symbolic breakpoints
You can create a symbolic breakpoint by pressing the + in the bottom left corner of the screen and then selecting Sybmolic breakpoint.

<p align="center">
<img src="https://raw.githubusercontent.com/xavipedrals/iosCheatSheet/master/create-symbolic-breakpoint.png" width="60%" margin="auto">
</p>


