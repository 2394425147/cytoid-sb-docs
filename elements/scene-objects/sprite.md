# Sprite

Sprite objects can load an image from the level folder and display it in the game.

{% hint style="info" %}
For best performance, keep the source image resolution below 1920px \* 1080px, and convert PNGs to JPGs when transparency is not needed.
{% endhint %}

## Properties

<table data-view="cards"><thead><tr><th>Key</th><th>Explanation</th><th data-type="select">Type</th></tr></thead><tbody><tr><td><code>path</code></td><td>Relative path to the image file. <br><br>For example, if the path is <code>"sprite.png"</code>, the file should be at the same location as the storyboard.json and named sprite.png. <br><br><code>.jpg</code> and <code>.png</code> are supported. </td><td></td></tr><tr><td><code>preserve_aspect</code></td><td><p>If <code>true</code>, the image aspect ratio is preserved. </p><p>Default: <code>true</code>.</p></td><td></td></tr><tr><td><code>color</code></td><td><p>Color tint of the sprite in the hex representation. </p><p>Default: <code>"#fff"</code> (untinted)</p></td><td></td></tr></tbody></table>

