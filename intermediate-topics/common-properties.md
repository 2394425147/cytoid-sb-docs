# Common Properties

Here's a brief overview of the common properties of states.

<table data-view="cards"><thead><tr><th>Key</th><th>Explanation</th><th data-type="select">Type</th></tr></thead><tbody><tr><td>id</td><td><p>A unique identifier of this object. </p><p>If not set, a random alphanumeric ID will be generated. </p><p>Supports the <code>$note</code> variable.</p></td><td></td></tr><tr><td><a href="common-properties.md#using-target_id">target_id</a></td><td><p><em><strong>For scene objects only.</strong></em> </p><p>When set, this object does not have its own entity form but controls the specified object instead. </p><p>The target object must be of the <strong>same type</strong>.</p><p>Supports the <code>$note</code> variable.</p></td><td></td></tr><tr><td><a href="common-properties.md#using-parent_id">parent_id</a></td><td><p><em><strong>For texts and sprites only.</strong></em> <br>When set, this object's movement follows the specified parent. (this object's position, rotation and scale will be attached to its parent) </p><p>Supports the <code>$note</code> variable.</p></td><td></td></tr><tr><td><a href="common-properties.md#using-time">time</a></td><td><p>The time at which this state should happen, measured in seconds. </p><p>This may not be equivalent to the true timing—see how an object's exact timing is calculated below.</p></td><td></td></tr><tr><td><a href="common-properties.md#using-relative_time">relative_time</a></td><td>The relative time to the parent state</td><td></td></tr><tr><td><a href="common-properties.md#using-add_time">add_time</a></td><td>The relative time to the last defined state.</td><td></td></tr><tr><td>easing</td><td><p>The easing used when animating this object from the current state to the next state. </p><p>See <a href="https://easings.net/">https://easings.net/</a> for more info.</p><p>Default: <code>linear</code>.</p></td><td></td></tr><tr><td><a href="common-properties.md#using-destroy">destroy</a></td><td><p>If <code>true</code>, this object is destroyed when it fully transitions into this state. </p><p>It is recommended to destroy an object when you do not need to use it anymore, for performance.</p></td><td></td></tr><tr><td><a href="common-properties.md#using-states">states</a></td><td>Extra states of this object.</td><td></td></tr></tbody></table>

For properties of individual objects, see [elements](../elements/ "mention").

***

## Usage Guide

### Using `target_id`

`target_id` is useful if you want to create animations that require **overlapping states**.&#x20;

For example, if you want to move a sprite in an arc, it is difficulty to achieve this with only one object, as easing can only be applied to all the properties in an object at once.&#x20;

You need two—one moves the sprite in the X direction with one easing, and another one moves the sprite in the Y direction with another:

```json
{
    "id": "sprite",
    "path": "dot.png",
    "time": 0,
    "x": 0,
    "easing": "linear",
    "states": [
        {
            "time": 5,
            "x": 200
        }
    ]
},
{
    "target_id": "sprite",
    "time": 0,
    "y": 0,
    "easing": "easeOutQuad",
    "states": [
        {
            "time": 5,
            "y": 200,
        }
    ]
}
```

Another example would be to simplify complex states.&#x20;

Say you want to move a text from `x = 0` at `t = 0` to `x = 100` at `t = 5`, while also setting its opacity from `a = 1` at `t = 2.5` to `a = 0` at `t = 7.5`.&#x20;

Without using a separate targeting scene object, you have to manually do some mental calculations to write down the 4 key states.

***

### Using `parent_id`

A fun thing to try is to set a sprite's parent to a note controller.&#x20;

Since a note controller has an implied position of the actual note, the sprite should follow the note's movement.

{% hint style="info" %}
_No, you can't really make custom skins with this yet._&#x20;

See [#using-usdnote-on-scene-objects](built-in-variables.md#using-usdnote-on-scene-objects "mention") for an in-depth explanation.
{% endhint %}

***

### Using `time`

{% hint style="warning" %}
If `time` is not set and this is a scene object (i.e. text or sprite), this scene object is **not spawned** unless manually spawned by a trigger.
{% endhint %}

This value can also be an array, if you want to create multiple identical states at once. For example:

```json
"states": [
	{
		"template": "pulse",
		"time": ["start:57", "start:123", "start:153"]
	}
]
```

is automatically expanded to

```json
"states": [
	{
		"template": "pulse",
		"time": "start:57"
	},
	{
		"template": "pulse",
		"time": "start:123"
	},
	{
		"template": "pulse",
		"time": "start:153"
	}
]
```

***

### Using `relative_time`

For example,

```json
{
	"time": 5,
	"states": [
		{
			// State A
			"relative_time": 2.5
		}
	]
}
```

The timing of state A would be `5` + `2.5` = `7.5`.

{% hint style="info" %}
if `relative_time` is defined, but there does not exist a parent state, the current state's time would be `current_game_time + relative_time`.

**This is intended for triggers.**
{% endhint %}

***

### Using `add_time`

For example,

```json
{
	"time": 5,
	"states": [
		{
			"relative_time": 2.5
		},
		{
			// State B
			"add_time": 3
		}
	]
}
```

The timing of state B would be (`5` + `2.5`) + `3` = `10.5`.

***

### Using `destroy`

In the following example along with the uses of triggers, the `Hello world!` text is spawned and displayed when note 4 is cleared, transitions into zero opacity before destroyed.

```json
...	
	"texts": [
		{
			"id": "hello_world",
			"text": "Hello world!",
			"size": 80,
			"opacity": 1,
			"states": [
				{
					"opacity": 0,
					"relative_time": 0.5,
					"destroy": true
				}
			]
		}
	],
	"triggers": [
		{
			"type": "noteClear",
			"notes": [4],
			"spawn": ["hello_world"]
		}
	],
...
```

***

### Using `states`

You can define states in an inner state, which will be appended to the parent object. For example:

```json
{
  ...
	Object definition
	...
	"states": [ // States defined in the parent object
		{
			"template": "stateA",
		},
		{
			"states": [ // States defined in an inner state
				{
					"template": "stateB"
				},
				{
					"template": "stateC"
				}
			]
		},
		{
			"template": "stateD"
		}
	]
}
```

is equivalent to

```json
{
  ...
	Object definition
	...
	"states": [
		{
			"template": "stateA",
		},
		{
			"template": "stateB"
		},
		{
			"template": "stateC"
		},
		{
			"template": "stateD"
		}
	]
}
```

This is useful when you want to reuse multiple states at once. See the `pulse` template in the storyboard example.
