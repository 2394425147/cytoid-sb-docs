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

| Key                   | Explanation                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Type |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---- |
| note                  | integer ID of the note, as defined in the chart file.                                                                                                                                                                                                                                                                                                                                                                                                           |      |
| override\_x           | if true, the x-coordinate of the note is overriden. See x, x\_multiplier and dx. Default false.                                                                                                                                                                                                                                                                                                                                                                 |      |
| x                     | <p>overridden x-coordinate of the note. Default coordinate system noteX.<br><br>You can unset this value by setting it to null.</p>                                                                                                                                                                                                                                                                                                                             |      |
| x\_multiplier         | multiplies onto the x-coordinate of the note. Default 1. Has no effect if x is already set.                                                                                                                                                                                                                                                                                                                                                                     |      |
| dx                    | adds onto the x-coordinate of the note. Default 0. Default coordinate system noteX. Has no effect if x is already set.                                                                                                                                                                                                                                                                                                                                          |      |
| override\_y           | if true, the y-coordinate of the note is overriden. See y, y\_multiplier and dy. Default false.                                                                                                                                                                                                                                                                                                                                                                 |      |
| y                     | <p>overridden y-coordinate of the note. Default coordinate system noteY.<br><br>You can unset this value by setting it to null.</p>                                                                                                                                                                                                                                                                                                                             |      |
| y\_multiplier         | multiplies onto the y-coordinate of the note. Default 1. Has no effect if y is already set.                                                                                                                                                                                                                                                                                                                                                                     |      |
| dy                    | adds onto the y-coordinate of the note. Default 0. Default coordinate system noteY. Has no effect if y is already set.                                                                                                                                                                                                                                                                                                                                          |      |
| override\_z           | if true, the z-coordinate of the note is overriden. See z. Default false.                                                                                                                                                                                                                                                                                                                                                                                       |      |
| z                     | overridden z-coordinate of the note. Default coordinate system depth.                                                                                                                                                                                                                                                                                                                                                                                           |      |
| override\_rot\_x      | if true, the rotation of the note on the x-axis is overriden. See rot\_x. Default false.                                                                                                                                                                                                                                                                                                                                                                        |      |
| rot\_x                | overridden rotation of the note on the x-axis in degrees. Default 0.                                                                                                                                                                                                                                                                                                                                                                                            |      |
| override\_rot\_y      | if true, the rotation of the note on the y-axis is overriden. See rot\_y. Default false.                                                                                                                                                                                                                                                                                                                                                                        |      |
| rot\_y                | overridden rotation of the note on the y-axis in degrees. Default 0.                                                                                                                                                                                                                                                                                                                                                                                            |      |
| override\_rot\_z      | if true, the rotation of the note on the z-axis is overriden. See rot\_z. Default false.                                                                                                                                                                                                                                                                                                                                                                        |      |
| rot\_z                | overridden rotation of the note on the z-axis in degrees. Default 0.                                                                                                                                                                                                                                                                                                                                                                                            |      |
| override\_ring\_color | if true, the ring color of the note is overriden. See ring\_color. Default false.                                                                                                                                                                                                                                                                                                                                                                               |      |
| ring\_color           | overridden ring color of the note. When set to null, user ring color is used. Default null.                                                                                                                                                                                                                                                                                                                                                                     |      |
| override\_fill\_color | if true, the fill color of the note is overriden. See fill\_color. Default false.                                                                                                                                                                                                                                                                                                                                                                               |      |
| fill\_color           | overridden fill color of the note. When set to null, user fill color is used. Default null.                                                                                                                                                                                                                                                                                                                                                                     |      |
| opacity\_multiplier   | multiplies onto the opacity of the note. Default 1.                                                                                                                                                                                                                                                                                                                                                                                                             |      |
| size\_multiplier      | multiplies onto the size of the note. Default 1.                                                                                                                                                                                                                                                                                                                                                                                                                |      |
| hold\_direction       | direction of the "tail" of a hold note; only applicable if note is a hold note. 1 is upwards and -1 is downwards. When set to null, original hold direction is used. Default null.                                                                                                                                                                                                                                                                              |      |
| style                 | <p>controls specific styling of the note; only applicable to hold notes for now. <code>1</code> and <code>2</code> are supported. Default <code>1</code>.<br></p><p><code>1</code>: The default style.</p><p><code>2</code>: The VSRG style. The triangle that connects the scanline and the hold note will be hidden; the tail becomes shorter as the hold note progresses; the clear effect will be played at the hold note, not the scanline's position.</p> |      |

## Usage Guide

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
