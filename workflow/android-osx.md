# Basic OS X Machine Setup for Android Development

## Easy mode

If you have [Homebrew](http://brew.sh/) and [Homebrew Cask](https://caskroom.github.io/):

```sh
brew cask install java
brew install android-sdk
brew cask install android-studio
```

Tested on El Capitan (OS X 10.11).

## Manual setup

> NB: These instructions are dated May 2015 and are for OS X 10.10.

####Pre-requisites
1. Update to Yosemite(OS X 10.10) from App Store
2. Install latest JRE at http://www.oracle.com/technetwork/java/javase/downloads/index.html
3. Android Studio still have dibs for Java 6 for its font rendering not to mention certain bugs with the latest OS X; Download this support patch https://support.apple.com/kb/DL1572 and install

####Setup Android Studio
1. Download and install it http://developer.android.com/sdk/index.html
2. Run Android Studio and follow throught the steps which includes downloading the rest of the dependencies such as Android SDK
