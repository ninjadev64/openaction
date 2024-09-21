## Manifest

Your plugin should contain a `manifest.json` file that supplies key information about your plugin to the OpenAction server. It should be present in the root of your plugin directory.

```ts
{
	// The human-readable name of your plugin. Required
	Name: string,
	// The user-facing author string (e.g. "ninjadev64"). Required
	Author: string,
	// The version of your plugin found in this directory. Required
	Version: string,
	// An icon to represent your plugin, relative to your plugin root. Required
	// This icon should be provided in PNG format, without the ".png" suffix. You may also provide @2x versions of this image.
	Icon: string,
	// The category for your plugin's actions to appear under.
	Category: string = "Custom",
	// The default path to your actions' property inspector.
	PropertyInspectorPath: string | null,
	// The actions provided by your plugin. Required
	Actions: [
		{
			// The name of this action. Required
			Name: string,
			// A unique identifier for this action. Required
			UUID: string,
			// A tooltip that sums up the purpose of this action.
			Tooltip: string = "",
			// An icon to represent this action, relative to your plugin root. Required if visible in action list
			// This icon should be provided in PNG format, without the ".png" suffix. You may also provide @2x versions of this image.
			Icon: string,
			// Whether or not to automatically toggle the state of this action on key up. Only applies to actions with two states.
			DisableAutomaticStates: boolean = false,
			// Whether or not this action should be visible in the action list.
			VisibleInActionsList: boolean = true,
			// Whether or not this action should be supported in Multi Actions.
			SupportedInMultiActions: boolean = true,
			// The path to this action's property inspector, if different to your plugin's default.
			PropertyInspectorPath: string = "<plugin default>",
			// The controllers this action should be supported on. Supported controllers are "Keypad" and "Encoder" (dials/sliders).
			Controllers: string[] = [ "Keypad" ],
			// The states that are part of this action. Required
			States: [
				{
					// The image of this state relative to your plugin root or "actionDefaultImage".
					Image: string = "actionDefaultImage",
					// The name of this state.
					Name: string = "",
					// The text to display on this state over the image.
					Title: string = "",
					// Whether or not to display the title over the image.
					ShowTitle: boolean = true,
					// The colour of the state title.
					TitleColor: string = "<server dependent>",
					// The vertical alignment of the state title, either "top", "middle", or "bottom".
					TitleAlignment: string = "middle",
					// The font style of the title, either "Regular", "Bold", "Italic", or "Bold Italic".
					FontStyle: string = "Regular",
					// The font size of the state title in pixels as rendered on a 72x72px state image.
					FontSize: string = "16",
					// Whether or not to underline the state title.
					FontUnderline: boolean = false
				}
			]
		}
	],
	// The operating systems your plugin is supported on. Required
	OS: [
		{
			// The platform in question. Can be "windows", "mac", or "linux". Note that "linux" is not supported by Stream Deck. Required
			Platform: string,
			// The minimum supported version of the platform in question.
			Version: string | null
		}
	],
	// The default path to your plugin executable file, relative to your plugin root.
	// HTML5 is supported if this value ends with the ".html" suffix, and Node.js if this value ends with either of the ".cjs" and ".mjs" suffixes.
	CodePath: string | null,
	// An override for CodePath on Windows.
	CodePathWin: string | null,
	// An override for CodePath on macOS.
	CodePathMac: string | null,
	// An override for CodePath on Linux.
	CodePathLin: string | null
}
```
