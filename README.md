# webpack hot dev client hmr fix
If you familier with [Create react app](https://github.com/facebook/create-react-app) and the [prefix bug](https://github.com/facebook/create-react-app/issues/3814), you come to right place!


## Over View
The problematic code: (link to the current file)
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


`react-utils` is a package and a part of `create react app` installation.

## Installation

```sh
npm i react-utils-hmr-prefix -D
```

