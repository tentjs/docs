# Passing data to components

In Tent, you can pass data to components by using custom attributes. Custom attributes are attributes that are not part of the standard HTML attributes.

```typescript
import { type Component, mount, tags } from "@tentjs/tent";

const { p } = tags;

const Greeting: Component = {
  view: ({ attr }) => {
    // `attr` returns the value of the attribute,
    // or `undefined` if the attribute is not present.
    // Therefore we provide a fallback message.
    const message = attr("message") ?? "No message";

    return p(message);
  },
};

mount(document.querySelector(".greeting"), Greeting);
```

And the HTML would look like this:

```html
<div class="greeting" message="Hello, world!"></div>
```

## Typed attributes

In reality all attributes are strings, but you can use the generic type on `attr<T>(name: string)` to provide type information.

```typescript
import { type Component, mount, tags } from "@tentjs/tent";

const { p } = tags;

enum Messages {
  Morning = "morning",
  Night = "goodbye",
}

const Greeting: Component = {
  view: ({ attr }) => {
    const message = attr<Messages>("message");
    // => `message` is of type `Messages | undefined`

    switch (message) {
      case Messages.Morning:
        return p("Hello, world!");
      case Messages.Night:
        return p("Goodbye, world!");
      default:
        return p("No message");
    }
  },
};

mount(document.body, Greeting);
```

The HTML:

```html
<div message="morning"></div>
```

## Passing data to nested components

You can pass data to nested components by using the attributes object on the element you are mounting the nested component to.

```typescript
import { type Component, mount, tags } from "@tentjs/tent";

const { div } = tags;

const Greeting: Component = {
  view: ({ attr }) => {
    // `who` is the attribute passed to the `Greeting` component.
    const who = attr("who") ?? "world";

    return div(`Hello, ${who}!`);
  },
};

const Parent: Component = {
  // `who` can be accessed in the `Greeting` component as an attribute.
  view: () => mount(div([], { who: "John" }), Greeting),
};

mount(document.body, Parent);
```
