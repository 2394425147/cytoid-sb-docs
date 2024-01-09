# Template

A template defines a set of default values to apply to an object.

For example, the following is a template that fades some text out over 3 seconds:

```json
"templates": {
		...,
		"my_awesome_template": {
			"text": "placeholder text",
			"size": 36,
			"opacity": 0,
			"easing": "EaseInOutQuad",
			"states": [
				{
					"opacity": 1,
					"relative_time": 0.5,
				},
				{
					"relative_time": 2.5
				},
				{
					"opacity": 0,
					"relative_time": 3
				}
			]
		}
}
```

{% hint style="info" %}
`templates` is a dictionary. A dictionary wraps its contents inside curly brackets `{}`.
{% endhint %}

Then, you can apply this template to any text:

```json
"texts": [
	...,
	{
		"text": "名も無い時代の集落の",
		"time": 23,
		"template": "my_awesome_template"
	}
},
```

You may have noticed that the `text` property is defined twice: Once in the template and once again in the real object.

Since a template only acts as a default value provider, the text shown in-game will take the value from the text object, i.e. `"名も無い時代の集落の"`.
