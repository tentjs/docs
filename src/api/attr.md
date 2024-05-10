# Attr

The `attr<T = string>(name: string)` function is used to get the value of an attribute from the component's element.

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
