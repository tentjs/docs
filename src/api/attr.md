# Attr

The `attr<T = string>(name: string)` function is used to get the value of an attribute from the component's element.

In other libraries/frameworks you might see this referred to as `props` or `properties`. But, since these are in fact just attributes on an element, they're called `attributes` in Tent.

```typescript
import { type Component, mount, tags } from "@tentjs/tent";

const { p } = tags;

const Greeting: Component = {
  view: ({ attr }) => {
    const message = attr("message");
    // => `message` is of type `string | undefined`

    return p(message ?? "Hello, world!");
  },
};

mount(document.body, Greeting);
```

## Typed attributes

In reality all attributes are strings, but you can use the generic type on `attr<T>(name: string)` to provide type information.

```typescript
import { type Component, mount, tags } from "@tentjs/tent";

const { p } = tags;

enum Messages {
  Warning = "warning",
  Error = "error",
  Success = "success",
}

const Message: Component = {
  view: ({ attr }) => {
    const message = attr<Messages>("message");
    // => `message` is of type `Messages | undefined`
    // defaults to `string` if no type is provided (`string | undefined`)

    switch (message) {
      case Messages.Warning:
        return p("Warning: Something went wrong!");
      case Messages.Error:
        return p("Error: Something went wrong!");
      case Messages.Success:
        return p("Success: Everything went right!");
      default:
        return p([]);
    }
  },
};

mount(document.querySelector(".message"), Message);
```
