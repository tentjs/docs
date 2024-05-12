# Stateful components

In Tent you can create stateful components by using the `state` property on the component object.

Here is an example:

```typescript
import { type Component, mount, tags } from "@tentjs/tent";

const { div, button } = tags;

type State = {
  count: number;
};

export const Counter: Component<State> = {
  state: { count: 0 },
  view: ({ state }) =>
    button(
      // Use the state with `state.X`
      `Clicked ${state.count} times`,
      // Update the state with an event listener
      { onclick: () => state.count++ },
    ),
};

mount(document.body, Counter);
```
