# EVRYTHNG-WS.JS (plugin for EVT.js)

**evrythng-ws.js** is an extension plugin to be used with [evrythng.js](https://github.com/evrythng/evrythng.js) or 
[evrythng-extended.js](https://github.com/evrythng/evrythng-extended.js) JS libraries.

It adds [MQTT over WebSockets](http://www.hivemq.com/blog/mqtt-essentials-special-mqtt-over-websockets) support to 
any resource, allowing to *publish*, *subscribe* and *unsubscribe* to the resource's topics easily.

**evrythng-ws.js** is available as a Bower package and uses [mqtt.js](https://www.npmjs.com/package/mqtt) library as a dependency.

## Installation

### Browser

##### With [Bower](http://bower.io/)

    bower install evrythng-ws --save
    
The Bower package is [AMD](http://requirejs.org/docs/whyamd.html)-compatible. This means you can load 
it asynchronously using tools like [Require.js](http://requirejs.org/) or simply dropping the script tag 
into your HTML page:

    <script src="bower_components/mqttjs-browserified/dist/mqtt.js"></script>
    <script src="bower_components/evrythng-ws/dist/evrythng-ws.js"></script>

**evrythng-ws.js** depends on [mqtt.js](https://www.npmjs.com/package/mqtt) external lib, 
which is installed automatically.

See [Usage](#usage) below for more details.

##### Load from CDN

Add the script tags into your HTML page:

    <script src="//cdn.rawgit.com/reitzemaj/mqttjs-browserified/master/dist/mqtt.js"></script>
    <script src="//cdn.evrythng.com/toolkit/evrythng-js-sdk/evrythng-ws-2.1.0.min.js"></script>
 
Or always get the last release:

    <script src="//cdn.evrythng.com/toolkit/evrythng-js-sdk/evrythng-ws.js"></script>
    <script src="//cdn.evrythng.com/toolkit/evrythng-js-sdk/evrythng-ws.min.js"></script>
    
For HTTPS you need to use:

    <script src="//d10ka0m22z5ju5.cloudfront.net/toolkit/evrythng-js-sdk/evrythng-ws-2.1.0.min.js"></script>
    <script src="//d10ka0m22z5ju5.cloudfront.net/toolkit/evrythng-js-sdk/evrythng-ws.js"></script>
    <script src="//d10ka0m22z5ju5.cloudfront.net/toolkit/evrythng-js-sdk/evrythng-ws.min.js"></script>

## Usage

#### RequireJS (AMD)

```javascript
requirejs.config({
    paths: {
        'mqtt': '../bower_components/mqttjs-browserified/dist/mqtt',
        'evrythng': '../bower_components/evrythng/dist/evrythng',
        'evrythng-ws': '../bower_components/evrythng-ws/dist/evrythng-ws'
    }
});
    
require(['evrythng', 'evrythng-ws'], function (EVT, WS) {

  EVT.use(WS);
  ...
  
});
```

#### Globals

```javascript
// The plugin is attached as EVT.WS
EVT.use(EVT.WS);
...
```

## Examples

#### General

Use specific settings (below are defaults):

```javascript
WS.setup({
  apiUrl: 'wss://ws.evrythng.com:443/mqtt',
  reconnectPeriod: 1000,
  keepAlive: 50,
  clientIdPrefix: 'evtjs'
});
```

Create a Device scope:

```
var device = new EVT.Device(DEVICE_API_KEY);
```

Subscribe to property updates on a device:

```javascript
device.property().subscribe(function(update) {
  console.log(update);
});
```

Subscribe to explicit location changes:

```javascript
device.location().subscribe(function(newLocation) {
  console.log(newLocation);
});
```

Publish property updates:

```javascript
device.property('key').publish(value);
```

Create an action:

```javascript
device.action('scans').publish();
```

Update a Thng:

```javascript
device.publish({
  name: 'My new cool name'
});
```

Unsubscribe to a subscribed topic:

```javascript
device.property().unsubscribe();
```

Alternatively use the Operator scope:

```javascript
var operator = new EVT.Operator(OPERATOR_API_KEY;

operator.product('{productId}').property().subscribe(function(update) {
  console.log(update);
});
```

---

## Documentation

Check all the available subscriptions on the [EVRYTHNG Pubsub documentation](https://developers.evrythng.com/docs/pubsub).

## Source Maps

Source Maps are available, which means that when using the minified version, if you open 
Developer Tools (Chrome, Safari, Firefox), *.map* files will be downloaded to help you debug code using the 
original uncompressed version of the library.

## Related tools

#### evrythng.js

[`evrythng.js`](https://github.com/evrythng/evrythng.js) is the core version of *evrythng.js* intended to be used in 
public applications and/or devices.

#### evrythng-extended.js

[`evrythng-extended.js`](https://github.com/evrythng/evrythng-extended.js) is an extended version of *evrythng.js* which 
includes Operator access to the API.

## License

Apache 2.0 License, check `LICENSE.txt`

Copyright (c) EVRYTHNG Ltd.
