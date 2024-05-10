# Nesting components

In Tent you can nest components by using the `mount` function inside the `view` method of another component.

```typescript
import { type Component, mount, tags } from "@tentjs/tent";

const { div } = tags;

const Child: Component = {
  view: () => {
    return div("I am a child component");
  },
};

const Parent: Component = {
  view: () => {
    return div([
      "I am a parent component",
      // The child component is mounted here
      // `div([])` is the element to which the child component is mounted.
      // It could be any element, like `span([])`
      mount(div([]), Child),
    ]);
  },
};

mount(document.body, Parent);
```

## You might not need to nest components

It is very common to think that everything has to be a component. This is something we've been taught by other frameworks. But, most of the time you don't need to nest components. You can simply use functions.

This example is a bit silly but you get the idea.

```typescript
import { type Component, mount, tags } from "@tentjs/tent";

const { div } = tags;

type Variants = "primary" | "secondary" | "tertiary";

const primary = () => div("I am the primary variant");

// Since child is not a component, we use lower case for the function name
const child = (variant: Variants) => {
  switch (variant) {
    case "primary":
      return primary();
    case "secondary":
      return div("I am the secondary variant");
    default:
      return primary();
  }
};

const Parent: Component<State> = {
  view: ({ attr }) => {
    const variant = attr("variant");

    return div([
      `I am a parent component, and the variant is ${variant}`,
      child(variant ?? "primary"),
    ]);
  },
};

mount(document.body, Parent);
```
