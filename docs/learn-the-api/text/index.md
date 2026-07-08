# Overview

## Introduction
The text system in CoshUI is built around `TextNode`-based widgets — `Label`, `Button`, `RichLabel`, and others — plus its own lightweight markup language called **CoshML**, inspired by BBCode. CoshML lets you style *parts* of a string by wrapping text in tags, rather than styling the whole Node uniformly.

---

## Text Properties

There are quite a few properties that let you change how text is rendered through CoshUI — text color, font, size, alignment, whether it wraps or hides when overflowing, and more. These apply to any `TextNode`, and set the *default* style for all the text on that Node.

To find the details, check the [Text Properties](text-properties.md) section.

---

## Fonts

Aside from setting a font directly on each Node, you can register your own fonts and change the font every `TextNode` falls back to by default.

To learn more, check the [Fonts](fonts.md) section.

---

## CoshML

If you need more than one style within a single string — like bolding a single word, or coloring part of a sentence — CoshML tags let you do that inline, without splitting text across multiple Nodes. This is primarily used through `RichLabel`.

To learn more, check the [CoshML](coshml.md) section.