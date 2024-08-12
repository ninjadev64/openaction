## Clientbound events

This page describes the events that can be sent by the OpenAction server to either plugins or property inspectors.

### keyDown

Fired on keypad key down.

**Received by:** Plugin

```ts
{
	event: string = "keyDown",
	// The action UUID supplied in the plugin manifest.
	// Utilise to determine which action was triggered.
	action: string,
	// A unique value to identify the instance.
	context: string,
	// A unique value to identify the device.
	device: string,
	payload: {
		// Instance settings as set using the `setSettings` event.
		settings: any,
		coordinates: {
			row: number,
			column: number
		},
		// The currently active state of this instance.
		state: number,
		// Whether or not this event was triggered as part of a Multi Action.
		isInMultiAction: boolean
	}
}
```

### keyUp

Fired on keypad key up.

**Received by:** Plugin

```ts
{
	event: string = "keyUp",
	action: string,
	context: string,
	device: string,
	payload: {
		settings: any,
		coordinates: {
			row: number,
			column: number
		},
		state: number,
		isInMultiAction: boolean
	}
}
```

### dialDown

Fired on encoder dial down.

**Received by:** Plugin

```ts
{
	event: string = "dialDown",
	action: string,
	context: string,
	device: string,
	payload: {
		settings: any,
		coordinates: {
			row: number,
			column: number
		},
		controller: string
	}
}
```

### dialUp

Fired on encoder dial up.

**Received by:** Plugin

```ts
{
	event: string = "dialUp",
	action: string,
	context: string,
	device: string,
	payload: {
		settings: any,
		coordinates: {
			row: number,
			column: number
		},
		controller: string
	}
}
```

### dialRotate

Fired on encoder dial rotate or encoder slider move.

**Received by:** Plugin

```ts
{
	event: string = "dialRotate",
	action: string,
	context: string,
	device: string,
	payload: {
		settings: any,
		coordinates: {
			row: number,
			column: number
		},
		controller: string,
		// For a dial, positive value signifies clockwise rotation, and a negative value signifies anticlockwise rotation.
		// The lowest position is set as 0, and highest position is set as 192.
		ticks: number,
		pressed: boolean
	}
}
```

### willAppear

Fired when the user switches to a profile containing this action, or a new instance of this action is created.

**Received by:** Plugin

```ts
{
	event: string = "willAppear",
	action: string,
	context: string,
	device: string,
	payload: {
		settings: any,
		coordinates: {
			row: number,
			column: number
		},
		controller: string,
		state: number,
		isInMultiAction: boolean
	}
}
```

### willDisappear

Fired when the user switches from a profile containing this action, or an instance of this action is removed.

**Received by:** Plugin

```ts
{
	event: string = "willDisappear",
	action: string,
	context: string,
	device: string,
	payload: {
		settings: any,
		coordinates: {
			row: number,
			column: number
		},
		controller: string,
		state: number,
		isInMultiAction: boolean
	}
}
```

### deviceDidConnect

Fired when a device is connected.

The Stream Deck software supplies an additional field, an integer to designate the model of Stream Deck in use.

**Received by:** Plugin

```ts
{
	event: string = "deviceDidConnect",
	device: string,
	deviceInfo: {
		name: string,
		size: {
			rows: number,
			columns: number
		}
	}
}
```

### deviceDidDisconnect

Fired when a device is disconnected.

The Stream Deck software supplies an additional field, an integer to designate the model of Stream Deck in use.

**Received by:** Plugin

```ts
{
	event: string = "deviceDidDisconnect",
	device: string
}
```

### propertyInspectorDidAppear

Fired when an action is selected and its property inspector appears.

**Received by:** Plugin

```ts
{
	event: string = "propertyInspectorDidAppear",
	action: string,
	context: string,
	device: string
}
```

### propertyInspectorDidDisappear

Fired when an action is deselected and its property inspector disappears.

**Received by:** Plugin

```ts
{
	event: string = "propertyInspectorDidDisappear",
	action: string,
	context: string,
	device: string
}
```

### titleParametersDidChange

Fired when the user changes the title parameters of an action.

```ts
{
	event: string = "titleParametersDidChange",
	action: string,
	context: string,
	device: string,
	payload: {
		settings: any,
		coordinates: {
			row: number,
			column: number
		},
		state: number,
		title: string,
		titleParameters: {
			fontFamily: string,
			fontSize: number,
			fontStyle: string,
			fontUnderline: boolean,
			showTitle: boolean,
			titleAlignment: string,
			titleColor: string
		}
	}
}
```

### didReceiveSettings

Fired in response to the `getSettings` event. Additionally fired to the plugin when the property inspector uses `setSettings`, and vice versa.

**Received by:** Plugin, Property inspector

```ts
{
	event: string = "didReceiveSettings",
	action: string,
	context: string,
	device: string,
	payload: {
		settings: any,
		coordinates: {
			row: number,
			column: number
		},
		isInMultiAction: boolean
	}
}
```

### didReceiveGlobalSettings

Fired in response to the `getGlobalSettings` event. Additionally fired to the plugin when the property inspector uses `setGlobalSettings`, and vice versa.

**Received by:** Plugin, Property inspector

```ts
{
	event: string = "didReceiveGlobalSettings",
	payload: {
		settings: any
	}
}
```

### sendToPlugin

Fired when the property inspector uses the `sendToPlugin` event.

**Received by:** Plugin

```ts
{
	event: string = "sendToPlugin",
	action: string,
	context: string,
	payload: any
}
```

### sendToPropertyInspector

Fired when the plugin uses the `sendToPropertyInspector` event.

**Received by:** Property inspector

```ts
{
	event: string = "sendToPropertyInspector",
	action: string,
	context: string,
	payload: any
}
```
