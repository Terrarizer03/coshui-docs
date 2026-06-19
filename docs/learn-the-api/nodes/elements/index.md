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

Now that we know the distinction, let's talk about the different kinds of `Elements` that CoshUI has.

---

## Button
`Button` is an atomic `Element` that displays text and comes with built-in hover and click animations out of the box. It automatically brightens on hover, darkens on press, and returns to its original color on release — all without any extra setup. It requires an `id` since it uses state to track its original background color for the animations.

If you want to learn more, check out the [Button](button.md) section.

---

## Label
`Label` is the simplest atomic `Element` in CoshUI. It displays a line of text and supports alignment, justification, overflow behavior, and custom fonts. It has no interaction behavior on its own, making it purely presentational.

If you want to learn more, check out the [Label](label.md) section.

---

## Checkbox
`Checkbox` is an atomic `Element` that toggles between a checked and unchecked state on click. It stores its state across frames and can be bound to a `Ref` to keep an external variable in sync with its value. 

!!! warning "Background Color Support" 
    Note that it does not support `background_color` animations since its background color is a direct representation of its checked state.

If you want to learn more, check out the [Checkbox](checkbox.md) section.

---

## Image
`Image` is an atomic `Element` that renders an image from a file path provided through its `src` property. It resolves the path to an absolute path at initialization and raises an error if the file doesn't exist. Beyond that it behaves like any other Node with support for sizing, transforms, and alpha.

If you want to learn more, check out the [Image](images.md) section.

---

## Slider
`Slider` is a composite `Element` that expands at runtime into a track and a draggable thumb. It supports a configurable value range, step snapping, and can be bound to a `Ref` to keep an external variable updated as the user drags. The thumb and track can each be targeted by their generated ids for animations.

If you want to learn more, check out the [Slider](slider.md) section.

---

## Dropdown
`Dropdown` is a composite `Element` that expands into a selector and a collapsible options list. It stores the selected index across frames, and when an item is selected it collapses the list and optionally updates a bound `Ref` with the chosen value. The selector and each option item have their own generated ids.

If you want to learn more, check out the [Dropdown](dropdown.md) section.