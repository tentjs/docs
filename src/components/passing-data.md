# Passing data to components

In Tent, you can pass data to components by using custom data-\* attributes. It's simple and easy to understand.

> **Note:** It's by design that `JSON.parse()` isn't called internally on all data attributes. You should be in full control of the data flow, and you should be explicit about what you expect.

```html
<div data-list='["foo", "bar", "baz"]' data-message="Hello, world!"></div>
```

```typescript
import { type Component, mount, tags } from "@tentjs/tent";

const { div, ul, li, p } = tags;

// This type will give your autocompletion in your editor,
// when using `el.dataset.X`. In this case it would suggest `list`, `message` and `amount`.
type Attrs = {
  list: string;
  message: string;
  amount: string;
};

// You could argue that `List` also shouldn't be a component,
// but for the sake of this example, let's keep it as a component.
const List: Component<{}, Attrs> = {
  view: ({ el }) => {
    // Cast the parsed string to an array of strings
    const list: string[] = JSON.parse(el.dataset.list);
    // No need to cast the message, since it's already defined as a string
    const message = el.dataset.message;
    // JSON.parse() will return a number, so no need to cast it
    const amount: number = JSON.parse(el.dataset.amount);

    return div([
      p(`The message is: "${message}"`),
      p(`The amount is: ${amount}`),
      ul(list.map((item, idx) => listItem(item, idx))),
    ]);
  },
};

// This is a pure function - it'll always return the same output for the same input.
// This makes it easy to test and reason about.
const listItem = (item: string, idx: number) => {
  return li(`Item ${idx}: ${item}`);
};

// In a real app, you would probably put `listItem` in a separate file.
export { List, listItem };
```
