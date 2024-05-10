# Attributes

In Tent, attributes are used to add properties to HTML elements. They are passed as the second argument to the tag functions.

```typescript
import { div } from "@tentjs/tent";

div("Hello, world!", { id: "my-element", class: "my-class" });
// => <div id="my-element" class="my-class">Hello, world!</div>
```

## Event listeners

To add event listeners you can use the standard event listener syntax.

```typescript
import { button } from "@tentjs/tent";

// onclick
button("Click me", {
  onclick: () => console.log("You clicked me!"),
});
// => <button>Click me</button>

// oninput
input({
  type: "text",
  oninput: (e) => console.log(e.target.value),
});
// => <input type="text" />
```

## Custom attributes

You can add custom attributes to elements.

Custom attributes are also used to pass data to components. You can read more about that in the [Passing data to components](./passing-data.md) section.

```typescript
import { div } from "@tentjs/tent";

div("Hello, world!", { "data-foo": "bar" });
// => <div data-foo="bar">Hello, world!</div>
```
