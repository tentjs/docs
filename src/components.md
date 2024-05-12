# Components

In Tent a component is a regular object with a `view` method.

```typescript
import { type Component, mount, tags } from "@tentjs/tent";

const { p } = tags;

const HelloWorld: Component = {
  view: () => {
    return p("Hello, world!");
  },
};

mount(document.body, HelloWorld);

// or, if you want to mount a component to all elements with a specific class,
// you can use `document.querySelectorAll` and `forEach`.

document.querySelectorAll(".hello-world").forEach((el) => {
  mount(el, HelloWorld);
});
```
