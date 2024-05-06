## Registration

The OpenAction server will start your plugin with arguments specifying the means of initialising the WebSocket connection. If you use a plugin SDK, such as openaction-rs, you may be able to skip these steps.

### Compiled plugin registration

Your plugin will be called with the following command-line argument format.

`yourplugin -port <port> -pluginUUID <uuid> -registerEvent <event> -info <info>`

Your plugin should initiate a WebSocket connection to the WebSocket server running on the specified port and send a registration event containing the supplied registration event and plugin UUID, similar to the procedure outlined for HTML5 plugins described below.

### HTML5 plugin registration

Your plugin should provide a function similar to the below to register the plugin with the OpenAction server. This function will be called automatically by the OpenAction server.

```js
function connectOpenActionSocket(port, pluginUUID, registerEvent, info) {
	const websocket = new WebSocket("ws://localhost:" + port);

	websocket.onopen = () => {
		websocket.send(JSON.stringify({
			"event": registerEvent,
			"uuid": pluginUUID
		}));
	};

	websocket.onmessage = (event) => {
		// Handle inbound events from the OpenAction server here
	};
}

// For Stream Deck compatibility
const connectElgatoStreamDeckSocket = connectOpenActionSocket;
```

### Property inspector registration

Your property inspectors should provide functions similar to the below to register themselves with the OpenAction server. These functions will be called automatically by the OpenAction server.

```js
function connectOpenActionSocket(port, propertyInspectorUUID, registerEvent, info) {
	const websocket = new WebSocket("ws://localhost:" + port);

	websocket.onopen = () => {
		websocket.send(JSON.stringify({
			"event": registerEvent,
			"uuid": propertyInspectorUUID
		}));
	};

	websocket.onmessage = (event) => {
		// Handle inbound events from the OpenAction server here
	};
}

// For Stream Deck compatibility
const connectElgatoStreamDeckSocket = connectOpenActionSocket;
```

### Info parameter

The info parameter supplied to both plugins and property inspectors is in the below format.

```ts
{
	application: {
		font: string,
		language: string, // e.g. "en"
		platform: string, // e.g. "mac"
		platformVersion: string, // e.g. "11.6.2"
		version: string // e.g. "OpenDeck 2.0.0"
	},
	plugin: {
		uuid: string, // e.g. "com.amansprojects.starterpack"
		version: string // e.g. "1.0.0"
	},
	devices: [
		{
			id: string,
			name: string,
			size: {
				rows: number,
				columns: number
			}
		}
	]
}
```

The Stream Deck software supplies additional fields in this parameter, such as an integer to designate the model of Stream Deck in use.
