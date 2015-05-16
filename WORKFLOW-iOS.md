# iOS Development Workflow

## Setting up a new project

1. Create a new project

    1. __File__ -> __New__ -> __Project__ or press `SHIFT + ⌘  + N` to create a new project.

    2. Choose __Single View Application__ then click Next.

    3. Type the __Name__ of your project.

    4. Type your __Organization Name__.

    5. Type your __Organization Identifier__. The naming convention for __Organization Identifier__ is reverse domain naming style (e.g. `net.proudcloud.ios.NowShowing`). The platform is included so we can also use this naming convention for Android ports of our apps, in this case `net.proudcloud.android.NowShowing`.

    6. Choose __Swift__ as the Language

    7. Choose the __Devices__ to support. Usually, it is just iPhone. Universal is selected when we need to support iPad.

2. Set up Build Number auto-updates

    1. Click on your project workspace. It is the row with the little blue file icon with your project's name, targets, and SDK version.

    2. Go to __Targets__ -> __Project Name__.

    3. Then in the __General__ panel, change the default __Version__ of the app to `0.0.1`.

    4. Then go to __Build Phases__.

    5. Add a new phase by clicking the `+` on the upper left corner of the panel then click __New Run Script Phase__.

    6. Collapse the newly added phase and paste the following:
        ```
        buildNumber=$(/usr/libexec/PlistBuddy -c "Print CFBundleVersion" "$INFOPLIST_FILE")
      buildNumber=$(($buildNumber + 1))
      /usr/libexec/PlistBuddy -c "Set :CFBundleVersion $buildNumber" "$INFOPLIST_FILE"
        ```
    7. Rename this phase to __Auto-update Build Number__ by double-clicking __Run Script__

    8. Then drag this new phase above __Copy Bundle Resources__ so that our build number is updated before `Info.plist` is copied to our archive. This ensures that the new archive has the updated build number.


3. Update the project structure

    Make sure you have the following project structure:
    ```
    ProjectName
  `- API
  `- Models
  `- Views
  `- Controllers
  `- Extensions
  AppDelegate.swift
  Images.xcassets
  Main.storyboard
  LaunchScreen.xib
  Supporting Files
  `- Info.plist
  `- BridgingHeader.h
    ```


4. Check-in your project to GitHub

    1. Initialize the project:
        ```
        $ git init
        ```

    2. Commit your changes:
        ```
        $ git add --all
        ```

    3. Set up the remote:
        ```
        $ git remote add origin <remote>
        ```

    4. Push your changes
        ```
        $ git push -u origin master
        ```


## Setting up CocoaPods

1. Go to your project's directory
    ```
    $ cd <ProjectName>
    ```

2. Create a new file named `Gemfile`.
    ```
    $ touch Gemfile && vim Gemfile
    ```

3. Add the following to your Gemfile:

    ```
    source 'https://rubygems.org'

  gem 'cocoapods'
    ```

4. Save and exit by typing `:wq`

5. Install CocoaPods by running:
    ```
    $ bundle install
    ```

6. When Bundler finishes installing CocoaPods, run:

    ```
    $ pod init
    ```

    This will create new file named __Podfile__ in your project directory. You can now add Pods in this file then run `pod install` to install them.


## Versioning

We'll follow the guidelines below as our versioning system.

Given we have the `x.y.z` as our version:

- We increment `z` when we publish bug fixes, and really small updates like changing a text.
- We increment `y` when we publish minor features that don't really affect the usage of the app.
- We increment `x` when we publish really big updates (e.g. major UI overhaul, breaking changes, etc.)

TLDR; `<major>.<minor>.<bugfixes>`

Also take note of our __Build Number__. The build number denotes how many times we've built the app by running (`⌘ + R`) or building the app (`⌘ + B`).

__NOTE:__ In cases where you have conflicts in the build number, always choose the higher build number.

## Branching

*TBA*

## Deployment

Follow the following steps to submit a build to the App Store.

1. Make sure __iOS Device__ is selected as your __Destination__. This should be similar to selecting your device to run your app on.
2. On Xcode's menu bar, Click __Product__ -> __Archive__. When this finishes, Xcode should automatically open the __Organizer__ window.
3. Click on the latest archive that you created, and click __Validate__. This validates your __*.ipa file__ (iOS application archive) for App Store submission.
    - (Optional) Fix errors in your build, if any.
4. If there are no errors in your build, click __Submit to App Store__ to submit your app. Additional checks will be done to your app and if it passes, your app is now uploaded to the App Store.
5. Login to __iTunes Connect__ to continue your submission.
6. Complete the app details, screenshots, and all required information to be able to submit.
7. Choose a build to submit.
8. (Optional) You may choose to publish your app manually or automatically, when your app passes the review process or manually publish
9. Click __Submit for Review__ and pray that your app passes the review process.

Your app should now say that it's __Waiting for Review__. This usually takes 1 to 2 weeks, and it's up to Apple now whether your app passes or gets rejected.


## Post-Deployment

After publishing your app, make sure you create a release tag for the new version you published.

For example, we've just published `v1.2.8` on the App Store

```
$ git tag v1.2.8
```

Then edit this release tag on GitHub and add the changes made in this build.
