# Nesting components

> Since `v0.0.25` you can't nest components. Instead you can create functions that return elements.

You can't nest components in Tent. This is by design.

Instead, you can use regular functions to create reusable parts of your UI. Fundamentally, it's almost the same, but it's more explicit, easier to understand, and much easier to test.

Given that Tent is built with the [Islands Architecture](https://www.patterns.dev/vanilla/islands-architecture) in mind, it makes sense to keep components as self-contained as possible. You're encouraged to keep your components small and focused on a single task.

## Example

```typescript
import { type Component, tags } from "@tentjs/tent";

const { ul, li } = tags;

type Attrs = {
  items: string; // JSON string with an array of strings
};

// You could argue that `List` also shouldn't be a component,
// but for the sake of this example, let's keep it as a component.
const List: Component<{}, Attrs> = {
  view: ({ attr }) => {
    // Cast the JSON string to an array of strings
    const items: string[] = JSON.parse(attr("items") ?? "[]");

    return ul(items.map((item, idx) => listItem(item, idx)));
  },
};

// This is a pure function - it'll always return the same output for the same input.
// This makes it easy to test and reason about.
const listItem = (item: string, idx: number) => {
  return li(`Item ${idx}: ${item}`);
};

// Export your `listItem` function so you can use it in other parts of your app.
// In a real app, you would probably put this in a separate file.
export { List, listItem };
```
