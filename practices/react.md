# React

## Suggested Setup of React:  

1. [Set up React Stack with Webpack](https://medium.com/proudcloud-dispatch/set-up-react-stack-with-webpack-3e510fb68ea8)
2. [Create React App CLI](https://github.com/facebook/create-react-app)

## Proposed File Structure
```
Project
└───public/
│   └───index.html
│   └───index.bundle.js        - output
└───src/
│   └───components/
│     └───App.js
│     └───Login.js
│     └───Home.js
│   └───index.js               - entry point
│   └───routes.js              - react-router routing
└───webpack.config.js          - webpack configuration
```

## Additional Tools

### API clients

1. Use [Apollo](https://www.apollographql.com/docs/react/essentials/get-started.html) for **GraphQL API**
2. Use [Fetch](https://facebook.github.io/react-native/docs/network.html) or [Axios](https://github.com/axios/axios) for **RESTful API**. See also [React-Redux](./react-redux.md)

### Use ES6 Spread Operator

Install: 
```
npm install --save-dev babel-plugin-transform-object-rest-spread

# or with yarn

yarn add babel-plugin-transform-object-rest-spread -D

```

Then add to your .babelrc
```
# inside .babelrc

{
  "plugins": ["transform-object-rest-spread"]
}
```

See: [BabelJS Doc](https://babeljs.io/docs/plugins/transform-object-rest-spread/)
