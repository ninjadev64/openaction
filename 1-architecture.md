## Architecture

OpenAction is an event-driven API that communicates over WebSocket.

Plugins provide actions, which can be instantiated by users on multiple profiles across multiple devices simultaneously. Each action instance is created from the properties specified in the plugin manifest, after which its states and settings can be mutated and these changes retained.

Each action may also be accompanied by a property inspector, a user interface displayed when the action is selected, where the user may customise the behaviour of the action. The `setSettings`, `getSettings`, `setGlobalSettings`, and `getGlobalSettings` events may be used by both the plugin and property inspector.

Users may also configure "Multi Actions", where multiple actions are executed in sequence.

Events are represented in (stringified) JSON format, with a field to identify the event and an optional payload containing more information about the event, as well as an instance context if the event is instance-related in order to identify it.

For more information about a specific event, consult the [clientbound events](4-clientbound.md) and [serverbound events](5-serverbound.md) pages.
