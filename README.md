# iOS Cheatsheet
Here's a list of things and commands that I use commonly when working in iOS.

## Carthage commands
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

### Gitignore
Configure a .gitgnore going to [gitignore.io](https://www.gitignore.io) and writing Xcode and Swift.

## Rx Swift (Reactive Programming)
Here you can find RxSwift and some examples https://github.com/ReactiveX/RxSwift.
For when default Rx table/collectionViews falls short https://github.com/RxSwiftCommunity/RxDataSources.
### RxMarbles
This let's you see in a super easy graphic way the manipulations you can do to an observable. I use it a lot.
http://rxmarbles.com

## iOS Assets (generate @3x, @2x)
To generate the image assets here you have an automator service that will be the best thing to generate @2x and @1x images from @3x images. 
http://kristian.co/2014/10/07/a-workflow-for-scaling-retina-assets.html
If you need to add @3x suffix to images names you can select multiple images and do a multiple rename.

