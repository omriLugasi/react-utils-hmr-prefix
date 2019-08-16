# webpack hot dev client hmr fix
If you familier with [Create react app](https://github.com/facebook/create-react-app) and the [prefix bug](https://github.com/facebook/create-react-app/issues/3814), you came to right place!

[![npm version](https://badge.fury.io/js/react-utils-hmr-prefix.svg)](https://badge.fury.io/js/react-utils-hmr-prefix)


## Over View
[The problematic code](https://github.com/facebook/create-react-app/blob/437b83f0337a5d57ce7dd976d2c3b44cb2037e45/packages/react-dev-utils/webpackHotDevClient.js#L60-L69):
```javascript
// Connect to WebpackDevServer via a socket.
var connection = new SockJS(
  url.format({
    protocol: window.location.protocol,
    hostname: window.location.hostname,
    port: window.location.port,
    // Hardcoded in WebpackDevServer
    pathname: '/sockjs-node',
  })
);

```
As you can see in the above code, the [sockJS](https://github.com/sockjs/sockjs-client) implementation is **Hard Coded** in the code, that's mean that you can't add prefix to your development hmr socket.

if you will try to use your app with prerix for example

`http://localhost:3000/prefix`

it's not gonna work, no metter how hard you will try.

`react-utils-hmr-prefix` will help you to accomplish the above with minimum changes.

## Installation

```sh
npm i react-utils-hmr-prefix -D
```

## requirements

- use eject ([link](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md))

## Implementation

**webpack.config.dev.js**
```javascript

require.resolve('react-dev-utils/webpackHotDevClient') // this line should be change to the line below
require.resolve('react-utils-hmr-prefix')

```

**env.js**

```javascript
 PUBLIC_URL: publicUrl,
 SOCK_JS_PREFIX: 'myCustomPrefix' //add this line to the file with your prefix
```


**public/index.html**

```html
 <!-- add this line into your head tag -->
 <meta id="dev-sock-js" content="%SOCK_JS_PREFIX%">
```

Those actions will create socket on yout origin + the custom prefix, for example `http://localhost:3000/myCustomPrefix`





