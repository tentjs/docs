# Tags

A `tag` in Tent is a function that returns an HTML element. Tent provides a set of built-in tags that you can use in your components, or you can create custom tags.

## Built-in tags

The full list of built-in tags can be found [here](../api/tags.md).

```typescript
import { tags } from "@tentjs/tent";

const { div, p, ul, li } = tags;

div("Hello, world!");
// => <div>Hello, world!</div>

p("Hello, world!");
// => <p>Hello, world!</p>

ul([li("Item 1"), li("Item 2"), li("Item 3")]);
// => <ul>
//      <li>Item 1</li>
//      <li>Item 2</li>
//      <li>Item 3</li>
//    </ul>
```

## Custom tags

Custom tags are useful when you want to create a tag that Tent doesn't provide.

For demonstration purposes, let's create a `strong` tag.

```typescript
import { createTag, type Children } from "@tentjs/tent";

const strong = (children: Children, attrs?: object) =>
  createTag(["strong", children, attrs]);

// Now we can use the `strong` tag, as any other tag.
strong("Hello, world!", { style: "color: pink;" });
// => <strong style="color: pink;">Hello, world!</strong>
```

### A real world example

```typescript
import { type Component, type Children, mount, tags } from "@tentjs/tent";

const { div, p } = tags;

const strong = (children: Children, attrs?: object) =>
  createTag(["strong", children, attrs]);

const HelloWorld: Component = {
  view: () => {
    return div(p(strong("Hello, world!")));
  },
};

mount(document.body, HelloWorld);
// => <div><p><strong>Hello, world!</strong></p></div>
// Of course, inside of the body element.
```
