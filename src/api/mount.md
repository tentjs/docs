# Mount

The mount function is used to append a component to the specified element.

```typescript
import { mount } from "@tentjs/tent";

const HelloWorld = {
  view: () => {
    return p("Hello, world!");
  },
};

mount(document.body, HelloWorld);
```
