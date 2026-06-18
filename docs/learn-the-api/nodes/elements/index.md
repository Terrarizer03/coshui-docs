# Overview

## Introduction
An `Element` is a Node with a specified behavior. They help with adding features and also optimizing certain combinations that are commonly done. 

An example of this is `Button`. Without this `Element`, users would have to nest a `Label` within a `Container` and create interactions for each, not to mention the edge cases like doing `mouse_filter=cui.IGNORE` on the `Label` so it doesn't consume interaction events. But with the `Button`, not only is that dealt with automatically, it saves a rendering pass because instead of going through 2 Nodes, it only goes through one.

---

## Atomic vs Composite

CoshUI has quite a few of these `Element` Nodes, and they can be categorized into 2 types. Atomic Nodes and Composite Nodes. 

Atomic Nodes mean they're a single Node, they're not a combination of 2 or more like how `Button` is just one Node and not a `Label` nested within a `Container`.

Composite Nodes are a little different, they're singular Nodes that get expanded into multiple at runtime. Here's an example, take this `Slider`:

```python title="Slider Example"
with cui.Container(...):
    cui.Slider(id="sldr")
```
You declare it like any other Node, just a singlular `Slider` declaration, but what CoshUI actually does when your code runs is **expand** that `Slider` Node into 2 Nodes:

```python title="Expanded Slider Example"
with cui.Container(...):
    with cui.Container(id="sldr::track"):
        cui.Box(id="sldr::thumb")

# NOTE:
# The "Box()" Node is not a public accessible node.
# It's kind of a redundant mistake I made
# that I'm too lazy to fix 
```
This splits the `Slider` into 2, the track and the thumb. A cool thing about this though is that these split Nodes now get their own ids, so if you were to animate something like `sldr::thumb` getting bigger, you can target that id and set its `transform_scale`.

Now that we know the distinction, let's talk about the different kinds of `Elements`that CoshUI has.

---

## Button

---

## Label

---

## Checkbox

---

## Image

---

## Slider

---

## Dropdown