# Note Selector

What if you want to control all flick notes, or all notes from ID 300 to 500?&#x20;

Note selectors come to the rescue!

A note selector is an JSON object (i.e. wrapped in `{}` braces) with following properties:

* **type**: array of acceptable note types. For example, `[3,4,6,7]` selects all drags and c-drags.
* **start**: minimum ID of the note.
* **end**: maximum ID of the note.
* **direction**: direction of the note's page. `1` indicates that this note is scanned upwards, and `-1` indicates that this note is scanned downwards.
* **min\_x**: minimum x-coordinate of the note.
* **max\_x**: maximum x-coordinate of the note.

Note selectors are best understood by thinking them as "filters" on notes. Following are some examples:

Select all click notes with ID ranged from 250-275:

```json
{
	"type": [0],
	"start": 250,
	"end": 275
}
```

Select all notes on the left side of the screen:

```json
{
  "min_x": 0,
  "max_x": 0.5
}
```

Select all notes which will be scanned by the scanline downwards:

```json
{
	"direction": -1
}
```

Select all notes (equivalently, apply no filters):

```json
{}
```

## Usage

To use a note selector, simply set it as the `note` of a predefined note controller:

```json
{
  "note": {
    "start": 7,
    "end": 9
  },
  "override_x": true,
  "x": 0.25
}
```

When loaded into the game, Cytoid filters the notes with the conditions defined in the selector. In this case, we know exactly 3 notes will be selected. This note controller is then automatically expanded into 3 note controllers:

```json
{
  "note": 7,
  "override_x": true,
  "x": 0.25
},
{
  "note": 8,
  "override_x": true,
  "x": 0.25
},
{
  "note": 9,
  "override_x": true,
  "x": 0.25
}
```

Which, as you expect, aligns the 3 notes at x = 0.25.

***

**An interesting detail**: you can actually use note selectors in other scene objects, such as sprites and texts.&#x20;

For example:

```json
{
...
	"sprites": [
		{
			"note": {},
			"path": "image.jpg"
		}
	]
...
}
```

This spawns an image for every note. Pretty useless, right?—You will see in a second how this will be useful in conjunction with the `$note` placeholder.
