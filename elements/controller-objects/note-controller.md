# Note Controller



A note controller overrides and animates the properties of a note in the chart .&#x20;

{% hint style="info" %}
This is the most powerful storyboard technique so far.&#x20;

You can implement almost any desired gameplay in Cytoid using note controllers!
{% endhint %}

{% hint style="warning" %}
As of 2.0.2, `size_multiplier` only works on clicks and flicks.
{% endhint %}

{% hint style="danger" %}
As of 2.0.2, `dx` and `dy` are incorrectly implemented, and you have to add 1 to the value you want to set for notes that are in a chart page of -1 direction.\
`dx` and `dy` will be replaced by `x_offset` and `y_offset` in the future.
{% endhint %}

<table data-view="cards"><thead><tr><th>Key</th><th>Explanation</th><th>Default</th></tr></thead><tbody><tr><td>note</td><td>integer ID of the note, as defined in the chart file.</td><td></td></tr><tr><td>override_x</td><td>if true, the x-coordinate of the note is overriden.</td><td>false</td></tr><tr><td>x</td><td>overridden x-coordinate of the note.<br>You can unset this value by setting it to null.</td><td>Default coordinate system: <code>noteX</code>.</td></tr><tr><td>x_multiplier</td><td><p>multiplies onto the x-coordinate of the note.</p><p>Has no effect if x is already set.</p></td><td>1</td></tr><tr><td>dx</td><td>adds onto the x-coordinate of the note.<br>Has no effect if x is already set.</td><td>0<br>Default coordinate system: <code>noteX</code>.</td></tr><tr><td>override_y</td><td>if true, the y-coordinate of the note is overriden.</td><td>false</td></tr><tr><td>y</td><td>overridden y-coordinate of the note.<br>You can unset this value by setting it to null.</td><td>Default coordinate system: <code>noteY</code>.</td></tr><tr><td>y_multiplier</td><td><p>multiplies onto the y-coordinate of the note. </p><p>Has no effect if y is already set.</p></td><td>1</td></tr><tr><td>dy</td><td><p>adds onto the y-coordinate of the note.</p><p>Has no effect if y is already set.</p></td><td>0<br>Default coordinate system: <code>noteY</code>.</td></tr><tr><td>override_z</td><td>if true, the z-coordinate of the note is overriden.</td><td>false</td></tr><tr><td>z</td><td>overridden z-coordinate of the note.</td><td>Default coordinate system: <code>depth</code>.</td></tr><tr><td>override_rot_x</td><td>if true, the rotation of the note on the x-axis is overriden.</td><td>false</td></tr><tr><td>rot_x</td><td>overridden rotation of the note on the x-axis in degrees.</td><td>0</td></tr><tr><td>override_rot_y</td><td>if true, the rotation of the note on the y-axis is overriden.</td><td>false</td></tr><tr><td>rot_y</td><td>overridden rotation of the note on the y-axis in degrees.</td><td>0</td></tr><tr><td>override_rot_z</td><td>if true, the rotation of the note on the z-axis is overriden.</td><td>false</td></tr><tr><td>rot_z</td><td>overridden rotation of the note on the z-axis in degrees.</td><td>0</td></tr><tr><td>override_ring_color</td><td>if true, the ring color of the note is overriden.</td><td>false</td></tr><tr><td>ring_color</td><td>overridden ring color of the note. <br>When set to null, user ring color is used. </td><td>null</td></tr><tr><td>override_fill_color</td><td>if true, the fill color of the note is overriden.</td><td>false</td></tr><tr><td>fill_color</td><td>overridden fill color of the note. <br>When set to null, user fill color is used.</td><td>null</td></tr><tr><td>opacity_multiplier</td><td>multiplies onto the opacity of the note.</td><td>1</td></tr><tr><td>size_multiplier</td><td>multiplies onto the size of the note.</td><td>1</td></tr><tr><td>hold_direction</td><td><p>direction of the "tail" of a hold note. </p><p>1 is up and -1 is down. <br>When set to null, original hold direction is used.</p></td><td>null</td></tr><tr><td><a href="note-controller.md#using-style">style</a></td><td><p>controls specific styling of the note; only applicable to hold notes for now.<br></p><p><code>1</code>: The default style.</p><p><code>2</code>: The VSRG style. The triangle that connects the scanline and the hold note will be hidden; the tail becomes shorter as the hold note progresses; the clear effect will be played at the hold note, not the scanline's position.</p></td><td>1</td></tr></tbody></table>

## Usage Guide

### Using `style`

To create vertical-scrolling style gameplay, simply set `override_y` to `true`, and animate `y` from `2` (or any value that is surely out of the vertical screen boundary) at time = `intro:$note` to `0` at time = `start:$note`.

In the [Interference: Finale](https://cytoid.io/levels/io.cytoid.interference3) EX storyboard, vertical-scrolling style gameplay is mixed with scanline gameplay. This is achieved by the charter first predefining a set of notes in the storyboard at a fixed X value, say, 0.4. Then the storyboarder uses a note selector that selects notes at X = 0.4 and animates them so that only they would fall onto the bottom of the screen, while other notes remain "normal."

{% hint style="info" %}
Due to accuracy issues of decimals, do not select notes at `X = 0.4` like this:

```json
{
	"min_x": 0.4,
	"max_x": 0.4
}
```

Instead, do:

```json
{
	"min_x": 0.39999,
	"max_x": 0.40001
}
```
{% endhint %}

To move a note in a curve, use two note controllers, one animates `x` and one animates `y`, each with different `easing` (for example, `easeInCirc` and `easeOutCirc` so that the note follows a trajectory of quarter of a circle).

***

Fix `y` to a constant value to mimic osu-style gameplay.
