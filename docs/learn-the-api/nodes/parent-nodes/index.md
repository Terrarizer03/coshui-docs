# Overview

## Introduction
`ParentNodes` are Nodes that let you build interesting UI structures inside CoshUI in a declarative way. They are context managers, meaning they automatically deal with adding the children nodes to their actual children list, setting those children's positions based on their parameters, and sometimes even determine how much space those children take up within them. 

When something like this:

```python title="ParentNode Example"
with cui.Container(...):
    cui.Button(...):
```
is done, CoshUI does one thing, it adds the `Container` to the global CoshUI stack, and once the `Button` is initialized, the Button adds itself to the children list of the recently added `ParentNode` in the stack. Once all children have been added, the `Container` then pops itself out of the stack, which then starts the entire cycle over for other `ParentNodes`.

So now that we know what `ParentNodes` do, let's talk about the 3 different kinds of `ParentNodes` that CoshUI has; `Container`, `Grid`, and `Modal`.

---

## Container
The `Container` is the most fundamental `ParentNode` in CoshUI. It arranges its children either in a row or a column depending on its `direction` property, and exposes properties like `align`, `justify`, `gap`, and `padding` to control how those children are spaced and positioned within it. Most layouts in CoshUI are built primarily out of nested `Container` nodes.

If you want to learn more, check out the [Container](containers.md) section.

---

## Grid
The `Grid` is a `ParentNode` designed for laying out children in a structured multi-column format. Unlike `Container`, it arranges children into a fixed number of columns set by the `column_count` property, automatically wrapping into new rows as needed. It's best suited for uniform, repeating layouts like galleries or dashboards.

If you want to learn more, check out the [Grid](grid.md) section.

---

## Modal
The `Modal` is a `ParentNode` designed for floating, draggable overlay panels. Unlike `Container` and `Grid`, it is a [composite node](../elements/index.md#atomic-vs-composite){ data-preview } — it expands internally into a header and a content area, where the header acts as a drag handle. It defaults to `ABSOLUTE` positioning, meaning it sits outside the normal document flow.

If you want to learn more, check out the [Modal](modal.md) section.