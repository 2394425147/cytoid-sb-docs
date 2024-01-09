---
description: Also known as scene controller.
---

# Controller

{% hint style="info" %}
You usually need only one controller to control the entire scene.

Multiple controllers will come in handy if you need to define effects with overlapping animation states.&#x20;

It's recommended to start with using only one controller.
{% endhint %}

## Properties

<table data-view="cards"><thead><tr><th>Key</th><th>Explanation</th><th>Default</th></tr></thead><tbody><tr><td>storyboard_opacity</td><td>opacity of all storyboard scene objects.</td><td><code>1</code></td></tr><tr><td>ui_opacity</td><td>opacity of the game UI (score, info, pause button...). </td><td><code>1</code></td></tr><tr><td>scanline_opacity</td><td>opacity of the scanline.</td><td><code>1</code></td></tr><tr><td>background_dim</td><td>opacity of the background dim.</td><td><code>0.85</code></td></tr><tr><td>note_opacity_multiplier</td><td>opacity of all notes will be multiplied by this value.</td><td><code>1</code></td></tr><tr><td>scanline_color</td><td>override the scanline color.</td><td><code>#ffffff</code> will be used when the chart is not changing speed, <code>#d25669</code> for speeding up, x for speeding down.</td></tr><tr><td>note_ring_color</td><td>override the ring color of all note.</td><td>user-defined ring color from settings</td></tr><tr><td><a href="controller.md#using-note_fill_colors">note_fill_colors</a></td><td>override the fill colors of different types of notes.</td><td>user-defined note color from settings</td></tr><tr><td>override_scanline_pos</td><td>if true, the y-coordinate of the scanline is overriden. </td><td><code>false</code></td></tr><tr><td>scanline_pos</td><td><p>overridden y-coordinate of the scanline. </p><p>0 is bottom, and 1 is top. </p><p>Out-of-bound values are also accepted.</p></td><td>Coordinate system: <code>noteY</code></td></tr><tr><td>perspective</td><td>Use perspective instead of orthographic <a href="https://discussions.unity.com/t/comparing-orthographic-and-perspective-cameras/169520/2">camera projection</a>.</td><td><code>false</code></td></tr><tr><td>size</td><td>Controls the viewport size of the orthographic camera.</td><td><code>5</code></td></tr><tr><td>fov</td><td>Controls the field of view of the perspective camera.</td><td><code>53.2</code></td></tr><tr><td>x</td><td>x-coordinate of the camera.</td><td><code>0</code><br>Coordinate system: <code>cameraX</code></td></tr><tr><td>y</td><td>y-coordinate of the camera.</td><td><code>0</code><br>Coordinate system: <code>cameraY</code></td></tr><tr><td>z</td><td>z-coordinate of the camera.</td><td><code>-10</code><br>Coordinate system: <code>depth</code></td></tr><tr><td>rot_x</td><td>rotation of the camera around the x-axis, measured in Euler angles.</td><td>0</td></tr><tr><td>rot_y</td><td>rotation of the camera around the y-axis, measured in Euler angles.</td><td>0</td></tr><tr><td>rot_z</td><td>rotation of the camera around the z-axis, measured in Euler angles.</td><td>0</td></tr><tr><td>chromatical</td><td>toggles the chromatical effect. </td><td>false</td></tr><tr><td>chromatical_fade</td><td>the transparency of the chromatical effect.</td><td></td></tr><tr><td>chromatical_intensity</td><td>the intensity of the chromatical effect. Ranged 0 to 1.</td><td></td></tr><tr><td>chromatical_speed</td><td>the speed of the chromatical effect. Ranged 0 to 3.</td><td></td></tr><tr><td>bloom</td><td>toggle the bloom effect.</td><td>false</td></tr><tr><td>bloom_intensity</td><td>Ranged 0 to 5.</td><td></td></tr><tr><td>radial_blur</td><td>toggle the radial blur effect.</td><td>false</td></tr><tr><td>radial_blur_intensity</td><td>Ranged -0.5 to 0.5.</td><td>0.025</td></tr><tr><td>color_adjustment</td><td>toggle color adjustment.</td><td>false</td></tr><tr><td>brightness</td><td>Ranged 0 to 10. </td><td>1</td></tr><tr><td>saturation</td><td>Ranged 0 to 10. </td><td>1</td></tr><tr><td>contrast</td><td>Ranged 0 to 10. </td><td>1</td></tr><tr><td>color_filter</td><td>toggle the screen color filter.</td><td>false</td></tr><tr><td>color_filter_color</td><td>color of the screen filter in the hex representation.</td><td></td></tr><tr><td>gray_scale</td><td>toggle the gray scale effect. Default</td><td>false</td></tr><tr><td>gray_scale_intensity</td><td>Ranged 0 to 1.</td><td></td></tr><tr><td>noise</td><td>toggle the noise effect.</td><td>false</td></tr><tr><td>noise_intensity</td><td>Ranged 0 to 1. </td><td>0.235</td></tr><tr><td>sepia</td><td>toggle the sepia effect.</td><td>false</td></tr><tr><td>sepia_intensity</td><td>Ranged 0 to 1.</td><td></td></tr><tr><td>dream</td><td>toggle the dream effect.</td><td>false</td></tr><tr><td>dream_intensity</td><td>Ranged 0 to 1.</td><td></td></tr><tr><td>fisheye</td><td>toggle the fisheye effect.</td><td>false</td></tr><tr><td>fisheye_intensity</td><td>Ranged 0 to 1. </td><td>0.5</td></tr><tr><td>shockwave</td><td>toggle the shockwave effect. </td><td>false</td></tr><tr><td>shockwave_speed</td><td>Ranged 0 to 10. </td><td>1</td></tr><tr><td>focus</td><td>toggle the focus (manga focus lines) effect. </td><td>false</td></tr><tr><td>focus_size</td><td>Ranged 1 to 10. </td><td>1</td></tr><tr><td>focus_color</td><td>Ranged 1 to 10. </td><td>1</td></tr><tr><td>focus_speed</td><td>Ranged 0 to 30. </td><td>5</td></tr><tr><td>focus_intensity</td><td>Ranged 0 to 1. </td><td>0.25</td></tr><tr><td>glitch</td><td>toggle the glitch effect.</td><td>fals</td></tr><tr><td>glitch_intensity</td><td>Ranged 0 to 1.</td><td></td></tr><tr><td>arcade</td><td>toggle the focus (manga focus lines) effect.</td><td>false</td></tr><tr><td>arcade_intensity</td><td>Ranged 0 to 1. </td><td>1</td></tr><tr><td>arcade_interference_size</td><td>Ranged 0 to 10. </td><td>1</td></tr><tr><td>arcade_interference_speed</td><td>Ranged 0 to 10. </td><td>0.5</td></tr><tr><td>arcade_contrast</td><td>Ranged 0 to 10. </td><td>1</td></tr><tr><td>tape</td><td>toggle the tape (screen flipping) effect.</td><td>false</td></tr></tbody></table>

## Usage Guide

### Using `note_fill_colors`

#### Format

`[click 1, click 2, drag 1, drag 2, hold 1, hold 2, long hold 1, long hold 2, flick 1, flick 2, c-drag 1, c-drag 2]`

The following example sets the color of all click notes to `#4568dc` and the color of all flick notes to `#000000`:&#x20;

```json
"note_fill_colors": [
    "#4568dc",   "#4568dc", 
    null,        null, 
    null,        null, 
    null,        null, 
    "#000000",   "#000000", 
    null,        null
]
```
