# Overview

## Introduction
CoshUI has a couple of Widgets or Nodes that make up the entire UI syntax. Overall, the types are split between 2 kinds, the `ParentNode` and the `Element`.

---

## ParentNode
A `ParentNode` is a type of Node that acts as a *context manager* and take in *children nodes*. It is the main system that drives the layout engine. An example of CoshUI's most basic and most used *`ParentNode`* is the `Container`:

```python title="Container Example"
with cui.Container(...):
    cui.Container(...)
```

A `ParentNode`, whether it be `Container`, `Grid`, or `Modal` can be treated as a *context manager* (`with` blocks). Although they can be treated as a regular `Element` on their own without the `with` block which stops them from taking in children nodes, their main purpose is to take in *children nodes*, determine their positions, and sometimes set how much space they take up.

If you want to learn more, check out the [Parent Nodes](parent-nodes/index.md) section.

---

## Element
An `Element` is a type of Node that generally lives as itself without having the ability to take in any *children nodes*. These are Nodes like `Button()` or `Label()` that don't drive layout and only really care about how they get presented.

```python title="Element Example"
with cui.Container(...):
    cui.Label(...)
    cui.Button(...)
```

`Elements` that are shown above are Widgets that have specific behavior. The label is an element that specifically displays text, while the Button both displays text and has default animation behaviors. Most `Element` Nodes can be approximated through primitives like the `Container` and custom signals, but they're specifically added to the library so rendering passes are not wasted.

If you want to learn more, check out the [Element Nodes](elements/index.md) section.