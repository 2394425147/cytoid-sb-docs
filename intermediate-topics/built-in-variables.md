# Built-in Variables

## Timing Variables

If the value is in one of the following formats, an automatic replacement will be performed. Note that the quotes are necessary. `<Note ID>` supports the `$note` placeholder (see the note controller section).

* `"start:<Note ID>"`: start time of the specified note
* `"end:<Note ID>"`: end time of the specified note
* `"intro:<Note ID>"`: intro time (i.e. when the note fades in) of the specified note
* `"start:<Note ID>:<Offset>"`: start time of the specified note + `<Offset>` (in seconds, can be negative)
* `"end:<Note ID>:<Offset>"`: end time of the specified note + `<Offset>` in seconds, can be negative)
* `"intro:<Note ID>:<Offset>"`: intro time (i.e. when the note fades in) of the specified note + `<Offset>` (in seconds, can be negative)
* 🌟 `"at:<Note ID>:<Percentage>"`: _for hold notes only._ start time of the specified note + (end time of the specified note - start time of the specified note) \* `<Percentage>`
  * When `<Percentage>` is `0`, this is equivalent to `start`
  * When `<Percentage>` is `1`, this is equivalent to `end`

## The `$note` Variable

It can be used in `id`, `parent_id`, `target_id` and `time`.\
Each occurrence will be replaced by the note ID in the current context. (Like a for loop)

For example, the code below applies a fading animation to note 100:

```json
{
	"note": 100,
	"opacity_multiplier": 1,
	"time": "intro:100",
	"states": [
		{
			"opacity_multiplier": 0,
			"time": "intro:100:0.2"
		}
	]
}
```

To apply this effect to all the notes, you can use `$note`:

```json
{
	"note": {},
	"opacity_multiplier": 1,
	"time": "intro:$note",
	"states": [
		{
			"opacity_multiplier": 0,
			"time": "intro:$note:0.2"
		}
	]
}
```

## Using `$note` on Scene Objects

The `$note` placeholder can be used in any other scene object.&#x20;

We just showed above how to spawn a sprite for every note, so let's see how to make them appear together with the note—or, custom note skins!

```json
{
...
	"note_controllers": [
		{
			"note": {},
			"id": "note_controller_$note",
			"time": 0,
			"opacity_multiplier": 0
		} // Creates a note controller for each note, each with a distinct id, and makes the note invisible
	],
	"sprites": [
		{
			"path": "image.jpg"
			"note": {}, // Spawn an image for each note...
			"parent_id": "note_controller_$note", // ...that locates and moves relative to the note (i.e. follows the note)
			"opacity": 0,			
			"time": "intro:$note", // ...that is hidden until the note appears
			"states": [
				{
					"opacity": 1,
					"time": "start:$note" // ...that becomes fully visible when the note is meant to be hit
				},
				{
					"add_time": 0.5,
					"destroy": true // Destroy after 0.5 seconds
				}
			]
		}
	]
...
}
```

That's a working note skin! But wait... All the sprites teleports to the center of the screen when we hit the notes. What's happening?

Turns out, when we hit the notes, the note controllers can no longer reference the notes' positions. Therefore, the sprites reset to their default position.

Although note controllers do not appear in the game, they actually have an implicit position, which is aligned with the position of their target note! Therefore, if you ever want to align some scene object with a note, just define a note controller for that note and set the parent of the scene object to the note controller.
