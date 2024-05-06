## Serverbound events

This page describes the events that can be sent by either plugins or property inspectors to the OpenAction server.

### setSettings

Used to set the settings value of an instance. When used by the plugin, the property inspector will receive a `didReceiveSettings` event, and vice versa.

**Sent by:** Plugin, Property inspector

```ts
{
	event: string = "setSettings",
	// A unique value to identify the instance.
	context: string,
	payload: any
}
```

### getSettings

Used to get the settings value of an instance. When used, the OpenAction server will respond with a `didReceiveSettings` event.

**Sent by:** Plugin, Property inspector

```ts
{
	event: string = "getSettings",
	context: string
}
```

### setGlobalSettings

Used to set the plugin-wide global settings value. When used by the plugin, all property inspectors will receive a `didReceiveSettings` event, and vice versa.

**Sent by:** Plugin, Property inspector

```ts
{
	event: string = "setGlobalSettings",
	payload: any
}
```

### getGlobalSettings

Used to get the plugin-wide global settings value. When used, the OpenAction server will respond with a `didReceiveSettings` event.

**Sent by:** Plugin, Property inspector

```ts
{
	event: string = "getGlobalSettings"
}
```

### openUrl

Used to open a fully-qualified URL in the user's default browser.

**Sent by:** Plugin, Property inspector

```ts
{
	event: string = "openUrl",
	payload: {
		url: string // e.g. "https://example.com/"
	}
}
```

### logMessage

Used to log a debug message to a log file. It is more strongly advised for plugin developers to handle logging on their own.

**Sent by:** Plugin

```ts
{
	event: string = "logMessage",
	payload: {
		message: string
	}
}
```

### setState

Used to switch an action to a state.

**Sent by:** Plugin

```ts
{
	event: string = "logMessage",
	payload: {
		// 0-based index specifying the state to be switched to.
		state: number
	}
}
```

### setTitle

Used to set the title of an instance.

**Sent by:** Plugin

```ts
{
	event: string = "setTitle",
	context: string,
	payload: {
		title: string,
		// 0: Both hardware and software, 1: Hardware only, 2: Software only
		target: number = 0,
		// 0-based index specifying the state to be modified.
		// If not set, the title will be applied to all states.
		state: number | null
	}
}
```

### setImage

Used to set the image of an instance.

**Sent by:** Plugin

```ts
{
	event: string = "setImage",
	context: string,
	payload: {
		// A base-64 data URL encoded image.
		image: string,
		// 0: Both hardware and software, 1: Hardware only, 2: Software only
		target: number = 0,
		// 0-based index specifying the state to be modified.
		// If not set, the image will be applied to all states.
		state: number | null
	}
}
```

### showAlert

Used to show a temporary alert indicator on the instance.

**Sent by:** Plugin

```ts
{
	event: string = "showAlert",
	context: string
}
```

### showOk

Used to show a temporary checkmark indicator on the instance.

**Sent by:** Plugin

```ts
{
	event: string = "showOk",
	context: string
}
```

### sendToPlugin

Fired by a property inspector to send a message to the plugin.

**Sent by:** Property inspector

```ts
{
	event: string = "sendToPlugin",
	action: string,
	context: string,
	payload: any
}
```

### sendToPropertyInspector

Fired by the plugin to send a message to a property inspector.

**Sent by:** Plugin

```ts
{
	event: string = "sendToPropertyInspector",
	action: string,
	context: string,
	payload: any
}
```
