# Positioning

## Coordinate Systems

The canvas for **storyboard** **sprites and texts**, or **stage**, has a resolution of 800 (width) \* 600 (height). (0, 0) is at the center. (400, 300) is the upper right corner. (-400, -300) is the lower left corner.

The X and Y axes are called `stageX` and `stageY`.

***

The canvas for **notes** use the same unit as in charts, spanning \[0, 1] in the X-axis and \[0, 1] in the Y-axis, where (0, 0) is the lower left corner.

The X and Y axes are called `noteX` and `noteY`.

***

The game **camera** has its own frame of reference based on its [orthographic size](https://docs.unity3d.com/ScriptReference/Camera-orthographicSize.html). By default, camera is positioned at (0, 0).

The X and Y axes are called `cameraX` and `cameraY`.

***

Finally, there is also an Z axis for parameters that are, well, on the game's **Z axis**, or, the depth axis. You do not care about this axis unless you have set **perspective** to true in a scene controller.

{% hint style="info" %}
The camera is looking at the +Z direction, and is by default at Z = -10. Setting a value like Z = -8 will put camera closer to the notes, while a value like Z = -15 will distance it away from the notes.
{% endhint %}

***

For any storyboard object property that uses a coordinate system above, you can **transform their coordinate systems** by using the following format: `[coordinate system]:[value]`.

## Examples

For example, say you have a sprite which you would like to display at the left of the bottom boundary of the gameplay/note area, which is exactly (0, 0) when expressed in noteX and noteY coordinate systems. However, the `x` and `y` values of a sprite by default use the stageX and stageY coordinate systems.

Before coordinate system transformations are introduced in 2.0.0, this is typically done by calculating the screen aspect ratio to estimate the corresponding coordinate in the stage canvas. This requires the storyboarder to create different storyboards for different screen aspect ratios (as seen [here](https://cytoid.io/levels/tigertiger.deadsoul)), and does not take into consideration that players can change their horizontal/vertical margins of the gameplay/note area.

Starting from 2.0.0, we can simply use coordinate system transformations to express the actual coordinate, like below:

```json
{
  ...
  Sprite definition
  ...
  "x": "noteX:0",
  "y": "noteY:0"
}
```

When the storyboard is loaded into the game, Cytoid automatically calculates the actual `x` and `y` values—without getting into the boring technical details, all you need to know is that the sprite will show up at the desired position of (0, 0) on the note canvas!

***

A more practical problem: how can we stretch a sprite to be a square such that its top and bottom are aligned to the screen boundaries?

A naive attempt would be:

```json
{
  ...
  Sprite definition
  ...
  "preserve_aspect": false, // Allow stretching of the sprite
  "width": 600,
  "height": 600
}
```

Unfortunately, this would not work: this is not necessarily a square. In fact, only devices with a 4:3 screen aspect ratio will render this as a square. Recall that the stage canvas resolution is 800 \* 600 on **any** device, so 1 unit in stageX does not necessarily equal 1 unit in stageY.

More simply put, when we set a sprite's `width` and `height` to be both 600, what we actually mean is that this sprite takes up 600/800=3/4 of the screen width and 600/600=all of the screen height. Therefore, to make it a square, 3/4 of the screen width must be equal to all of the screen height, which enforces a 4:3 screen ratio.

To align the square with top and bottom boundaries of the screen, the `height` necessarily equals `600`; the problem stems from our defined `width`. So what went wrong? **We assumed 1 unit of `width` (stageX) is equal to 1 unit of `height` (stageY),** which we now know is not the case. Then, if we can somehow make `width` use the same unit as `height`...

```json
{
  ...
  Sprite definition
  ...
  "preserve_aspect": false,
  "width": "stageY:600",
  "height": 600
}
```

And that is it! We delegated the calculation to Cytoid—`stageY:600` means 600 units in the stageY coordinate system. Whatever that value is, this has made sure our sprite will stretch to a square.

***

You should probably not transform any value to/from the depth coordinate system, as it does not make mathematical sense. But you can do it nonetheless! Feel free to try. 😇
