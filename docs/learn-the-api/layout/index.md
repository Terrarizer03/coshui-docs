# Overview

When making a `Node`, there are certain properties that affect CoshUI's layout engine. Here are the specific attributes that you need to know.

---

### Width and Height

```python
with cui.Container(id="example_container", width=100, height=100):
```

Width and height are a no-brainer; they're the attributes that set the size of the `Node`. If you want to learn more about how these attributes work and their default behaviors, [click here.](width-and-height.md)

### Padding and Margin

```python
with cui.Container(id="example_container", padding=10, margin=10):
```

Padding and Margin — a staple in UI systems — are attributes that set the space outside and within a `Node`. To learn more about how they work and their default behavior, [click here.](padding-and-margin.md)

### Position (x and y)

```python
with cui.Container(id="example_container", position=cui.ABSOLUTE, x=10, y=10):
```

Position is a special attribute in CoshUI. This is one of the attributes that can only be set under certain circumstances. To learn more, [click here.](position.md)

### Positioning

```python
with cui.Container(id="example_container", position=cui.ABSOLUTE):
```

Postioning is the attribute that determines whether a `Node` is added to the normal layout calculations or taken out out of it. If you want to understand it deeply, it's best to check out the **"Position (x and y)"** section above this section and [this page.](absolute-vs-relative.md)

### Align and Justify

```python
with cui.Container(id="example_container", align=cui.ALIGN_START, justify=cui.JUSTIFY_END):
```

Align and Justify determines the initial position and gap of/between Nodes. It's a very primitive and limited implementation as of version {{ version }}, so to learn the specific implementations, [click here.](align-and-justify.md)