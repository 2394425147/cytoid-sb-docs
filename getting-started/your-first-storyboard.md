---
description: >-
  To follow this guide, you'll need to have CytoidPlayer already downloaded and
  extracted into a folder on your computer, and the AmazingBomb starter kit set
  up.
---

# Your First Storyboard

With the CytoidPlayer app open, in the `player` folder, find and open the `storyboard.json` file.

It may seem complicated at first, but really it can be broken down into a structure like this:

```json
{
    "texts": [ 
        ... 
    ],
    "sprites": [ 
        ... 
    ],
    "controllers": [
        ...
    ],
    "templates": {
        ...
    },
}
```

For now though, we can just delete everything.

In the blank document, write:

<pre class="language-json" data-full-width="false"><code class="lang-json">{
    "texts": [
        {
            "text": "Hello world!",
            "time": 0,
            <a data-footnote-ref href="#user-content-fn-1">"opacity": 1</a>
        }
    ]
}
</code></pre>

You might be wondering, why is a pair of curly brackets `{}` wrapping around everything?

In JSON, a block of code wrapped by curly brackets is called an **object**, it's like a box that contains some data.

For example, the code below is a JSON object:

<pre class="language-json" data-full-width="false"><code class="lang-json">{
    <a data-footnote-ref href="#user-content-fn-2">"key"</a>: <a data-footnote-ref href="#user-content-fn-3">"value"</a>
}
</code></pre>

Go ahead and hit `CTRL` + `S` to save the file, and you should be able to see the text in CytoidPlayer.

Congratulations, that was your first storyboard!&#x20;

## More About JSON

What are the pair of `"text"` <mark style="color:yellow;">`:`</mark> `"Hello world!"` doing here?

We call these **key-value pairs**. In here, we're setting the property `text` to `Hello world!`

Let's move the text a bit higher! After `"Hello world!"`, add a comma `,` to indicate there's another property, and add a new line:

```json
{
    "text": "Hello world!",
    "time": 0,
    "opacity": 1
    "y": 0.5
}
```

Keep in mind that `0.5` isn't surrounded by quotation marks. This means that you **don't** want to use it as literal text.

You should see the text being positioned a bit higher than before. Mess around and see what else you can get!

You might have also noticed that the values for `"texts"` or `"sprites"` are not objects, but rather some type of block that contains **multiple objects**. These are called **arrays**. For example, `"texts"` contains multiple text objects.

Here's a non-exhausting list of acceptable values:

<table><thead><tr><th width="185">Type</th><th>Example</th></tr></thead><tbody><tr><td>String / Text</td><td><code>"text"</code></td></tr><tr><td>Number</td><td><code>1</code> <code>1.5</code> <code>-.5</code> (The leading <code>0</code> in <code>-0.5</code> can be omitted)</td></tr><tr><td>Boolean</td><td><code>true</code> <code>false</code> (A boolean value can only be one of these two)</td></tr><tr><td>Object</td><td><code>{ ... }</code></td></tr><tr><td>Array</td><td><code>[ ... ]</code></td></tr></tbody></table>



[^1]: Opacity of text elements are by default 0, (invisible), so we need to set it to 1 so it's visible. Learn more [here](../elements/scene-objects/).

[^2]: This means that the `key` component of this key-value pair is "key"

[^3]: This means that the `value` component of this key-value pair is "value"
