# React Redux

## Containers vs Components
- Containers are smart components. They do data-fetching and pass it to components.
- Components are dumb and reliant to containers for their data. Since they are relaint to containers, they can be reused in other containers.
- [Making your app fast with high-performance components by Jason Bonta](https://youtu.be/KYzlpRvWZ6c?t=22m49s)

## Suggested File structure

The suggested file structure is based on @adimasuhid's idea. If you have a directory and it was removed, the app should be still functional or needs minimal changes to make it work.

This also allows reusable features through other applications such as `chat` and `filtering`.

```
react
└───(Feature)
│   └───components
│   └───containers
│   │   actions.jsx            - action creator functions
│   │   actionTypes.jsx
│   │   apiWrappers.jsx
│   │   reducer.jsx            - reducer to be used in the store
│   │   propTypes.jsx          - reusable proptypes
└───(Shared Components)
└───App.jsx                    - main entrypoint
└───configureStore.jsx         - store builder
└───DevTools.jsx
└───rootReducer.jsx
```

## `mapStateToProps`, `mapDispatchToProps` and `connect`

There are some examples in the `redux` repository that show you can use a function for getting the object needed for `mapStateToProps`. We recommend that you use this example below for verbosity.

```js
const mapStateToProps = (state) => {
  return {
    component: state.component.attribute
  }
}
```

`mapDispatchToProps` can be omitted unless you want to.  It can be written like this:

```js
const mapDispatchToProps = (dispatch) => {
  return {
    function:  () => { namedFunction() }
  }
}

export default connect(
  mapStateToProps,
  mapDispatchToProps
)(Container)
```

or

```js
export default connect(
  mapStateToProps,
  { namedFunction }
)(Container)
```

## Configuring the Store

The `compose` function allows you to add different middlewares such as `redux-thunk` and `redux-devtools`.

```js
export default configureStore(initialState = {}, environment) => {
  const store = createStore(
    rootReducer,
    initialState,
    compose(
      applyMiddleware(thunk)
    )
  )
}
```

Here are some middlewares you might want to check out:
- [redux-thunk](https://github.com/gaearon/redux-thunk)
- [redux-saga](https://github.com/yelouafi/redux-saga)
- [redux-promise-middleware](https://github.com/pburtchaell/redux-promise-middleware)

See [this StackOverflow answer](http://stackoverflow.com/questions/36577510/what-is-the-difference-between-redux-thunk-and-redux-promise) on the difference between redux-thunk and redux-promise.
