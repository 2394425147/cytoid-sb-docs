# State

States are like keyframes in animation software. They define the properties of an object from different moments in time.

Here's an example, click on the underlined code to see what they are:

<pre class="language-json"><code class="lang-json">{
    "text": "Hello states!",
    <a data-footnote-ref href="#user-content-fn-1">"y": 0</a>,
    <a data-footnote-ref href="#user-content-fn-2">"states"</a>: [
        {
            <a data-footnote-ref href="#user-content-fn-3">"time": 1</a>,
            <a data-footnote-ref href="#user-content-fn-4">"y": -0.5</a>
        }
    ]
}
</code></pre>

## The Initial State

Every defined object has at least one state, which is the initial state.

In the code above, this is its initial state:

```json
{
    "text": "Hello states!",
    "y": 0,
}
```

[^1]: We define a starting `y` position of 0

[^2]: The `states` object stores all the states of its belonging object.

[^3]: This state stores the properties this object should have at the time of `1` second into the song.

[^4]: The text will move from (0, 0) to (0, -0.5) over the span of `1` second.
