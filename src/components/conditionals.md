# Conditionals

Since the `view()` method on a component is just a regular function, you can use regular if/else statements, or the ternary operator, to conditionally render elements.

```typescript
import { type Component, mount, tags } from "@tentjs/tent";

const { div, button } = tags;

type State = {
  easy: boolean;
};

const Conditionals: Component<State> = {
  state: { easy: true },
  view: ({ state }) =>
    div([
      button("Toggle", { onclick: () => (state.easy = !state.easy) }),
      p(state.easy ? "This is easy, right?" : "Damn, I thought so."),
    ]),
};

mount(document.querySelector(".recipe"), Conditionals);
```

Or, you can add the braces to the view function, and create a variable to hold the text, and use a regular if statement.

```typescript
import { type Component, mount, tags } from "@tentjs/tent";

const Conditionals: Component<State> = {
  state: { easy: true },
  view: ({ state }) => {
    let text = "";

    if (state.easy) {
      text = "This is easy, right?";
    } else {
      text = "Damn, I thought so.";
    }

    return div([
      button("Toggle", { onclick: () => (state.easy = !state.easy) }),
      p(text),
    ]);
  },
};

mount(document.querySelector(".recipe"), Conditionals);
```
