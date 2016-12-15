# React Native

This is a collection of (best?) practices when developing React Native apps--the Proudcloud way.

Basic prerequisites of developing React Native apps include [React](https://facebook.github.io/react/)
and [Redux](http://redux.js.org/). If you don't even have a slightest clue on what you're doing, STOP.
Please do us a favor: read [Thinking In React](https://facebook.github.io/react/docs/thinking-in-react) 
and create sample apps before even jumping on-board a project. This will save us time spent on nonsense
code reviews.

## Proposed File Structure

Given that we have a Blog app with basic CRUD functionalities, below is its proposed file structure:

```
project
`- android                  - Android Studio project
`- ios                      - Xcode project
`- js
   `- actions
      `- post.js
      `- user.js
   `- assets
      `- fonts
      `- images
      `- ...
   `- components
      `- common             - Shared components like forms, buttons, etc.
         `- Button.js
         `- FacebookButton.js
         `- ...
      `- PostList.js
      `- PostDetails.js
      `- RegistrationForm.js
      `- LoginForm.js
      `- ...
   `- config
      `- index.js            - You can probably load environment variables in this file
      `- facebook.js         - Sample Facebook-related config. You can load this in config/index.js
   `- containers
      `- posts
         `- New.js
         `- Edit.js
         `- List.js
      `- sessions
         `- Registration.js
         `- Login.js
   `- reducers
      `- index.js            - This is the root reducer
      `- posts.js
      `- users.js
   `- store
      `- configureStore.js
   `- utils                  - Any utility classes/helpers go here
   App(.ios/.android).js     - Main React class. Omit .ios or .android as necessary
`- node_modules
index.android.js
index.ios.js
package.json
```

## Containers vs. Components

As mentioned in https://github.com/proudcloud/awesome/blob/master/practices/react-redux.md

> Separate your containers from your components.

> - Containers are smart components. They do data-fetching and pass it to components.
> - Components are dumb and reliant to containers for their data. Since they are relaint to containers, they can be reused in other containers.

> See: [Making your app fast with high-performance components by Jason Bonta](https://youtu.be/KYzlpRvWZ6c?t=22m49s)

Or in iOS Development terms, think of Containers as View Controllers and Components as separate Views.


## Further Reading

Here are great articles for further reading:
- [React Native Getting Tutorial](https://facebook.github.io/react-native/docs/tutorial.html)
- [React Native Awesome](https://github.com/enaqx/awesome-react#react-native)
- [Building the F8 2016 App](http://makeitopen.com/)
- [Preview your React Native apps in your Github Pull Request](http://tech.m6web.fr/preview-android-ios-react-native-on-github-pull-request/)


## Deep Dive

If you need a good jumpstart, try following [Building the F8 2016 App](http://makeitopen.com/).
It's a great starting point for begginers and a good refresher for intermediate React Native developers.
