# The view

The `view` method is the only required method in a Tent component. It is a function that returns exactly one root element.

Whenever the state of a component changes, the `view` method is called again, and the new element is compared with the previous one. If they are different, the component is re-rendered.

```typescript
import { type Component, mount, tags } from "@tentjs/tent";

const { div, p, button } = tags;

type State = {
  count: number;
  clicked: boolean;
};

const HelloWorld: Component<State> = {
  state: { count: 0, clicked: false },
  view: ({ state }) => {
    // You can use regular JS here.
    // It is just a regular function.

    // You can define variables like this.
    // They will be re-evaluated on every render.
    const foo = "bar";

    // You can define event handlers like this,
    // or, inline in the element.
    const handleClick = () => {
      // You can update the state like this.
      state.count++;

      // or, like this for regular assignment.
      state.clicked = true;
    };

    // You have to return exactly one root element.
    // It can have any number of children.
    return div([
      p("Hello, world!"),
      p(`Foo is ${foo}`),
      div([
        p("This is a nested element."),
        state.clicked ? p("You clicked the button.") : p([]),
        p(`And also use state values: ${state.count * 2}`),
      ]),
      p(`Count is ${state.count}`),
      button("Click me!", { onclick: handleClick }),
    ]);
  },
};

mount(document.body, HelloWorld);
```
