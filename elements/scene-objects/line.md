# Line

A line object renders connected line segments. You can use it to mimic a scanline or draw any geometry shape, like a triangle.

{% hint style="warning" %}
Only a very limited subset of parameters in the scene object state are supported: opacity, layer and order.
{% endhint %}

## Properties

<table data-view="cards"><thead><tr><th>Key</th><th>Explanation</th><th data-type="select">Type</th></tr></thead><tbody><tr><td><a href="line.md#using-pos">pos</a></td><td>array of vertex objects</td><td></td></tr><tr><td>width</td><td>width of the line segments. Default 0.05.</td><td></td></tr><tr><td>color</td><td>color of the line segments in the hex representation. Default "#fff" (white).</td><td></td></tr></tbody></table>

## Usage Guide

### Using `pos`

Each vertex is a JSON object with following properties:

<table data-view="cards"><thead><tr><th>Key</th><th>Explanation</th><th data-type="select">Type</th></tr></thead><tbody><tr><td><code>x</code></td><td>x-coordinate of the vertex.<br>Default coordinate system: <code>noteX</code>.</td><td></td></tr><tr><td><code>y</code></td><td>y-coordinate of the vertex.<br>Default coordinate system: <code>noteY</code>.</td><td></td></tr><tr><td><code>z</code></td><td>z-coordinate of the vertex.<br>Default coordinate system: <code>depth</code>.</td><td></td></tr></tbody></table>

## Example

An example to animate a triangle using two line states:

```json
{
  "time": 0,
  "opacity": 1,
  "pos": [
    {
      "x": 0,
      "y": 0
    },
    {
      "x": 1,
      "y": 0
    },
    {
      "x": 0,
      "y": 1
    },
    {
      "x": 0,
      "y": 0
    }
  ],
  "states": [
    {
      "time": 20,
      "pos": [
        {
          "x": 0,
          "y": 1
        },
        {
          "x": 1,
          "y": 0
        },
        {
          "x": 1,
          "y": 1
        },
        {
          "x": 0,
          "y": 1
        }
      ]
    }
  ]
}
```

Try this yourself and figure out why the triangle animates like that! 😉
