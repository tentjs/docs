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
```

### Mounting to multiple elements

If you'd like to mount a component to multiple elements, you simply loop over the elements and call `mount` for each element.

```typescript
document.querySelectorAll(".hello-world").forEach((el) => {
  mount(el, HelloWorld);
});
```
