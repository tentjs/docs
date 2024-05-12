# Mount

```typescript
mount<S extends {} = {}>(
  element: HTMLElement | Element | TentNode | null,
  component: Component<S>,
)
```

The `mount` function is used to append a component to the specified element. The element can be an element in the document, or an element returned by a `tag` function.

```typescript
import { type Component, mount, tags } from "@tentjs/tent";
import { Child } from "./components/Child";

const { div, p } = tags;

const HelloWorld = {
  view: () =>
    div([
      p("Hello, world!"),
      // Mount the `Child` component to the `div` element.
      mount(div([]), Child),
    ]),
};

mount(document.body, HelloWorld);
```
