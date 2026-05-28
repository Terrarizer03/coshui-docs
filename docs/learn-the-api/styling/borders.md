# Borders

### Quick Guide

| Property | Type | Default | Recursive or Local |
| :--- | :--- | :--- | :--- |
| `border` | tuple(tuple(r, g, b), weight) **or** tuple(r, g, b, weight) | None | Local | 

### Introduction

Borders in CoshUI act as the *outline* of rectangles. When setting a border, it naturally takes in the `color` of that border and the `weight`. You can set it in 2 ways, like this:

```python title="Setting border"
with cui.CoshUIRenderer(...):
    cui.Container(id="example_container", style=cui.CoshStyling(border=((255, 0, 0), 5)))
# or
with cui.CoshUIRenderer(...):
    cui.Container(id="example_container", style=cui.CoshStyling(border=(255, 0, 0, 5)))
```

The border that's set above will be a <span style="color: #ff0000;">red</span> border with a weight of 5 pixels.

### Default Behavior

The default behavior of `border` is `None`.

```python title="Default Behavior"
with cui.CoshUIRenderer(...):
    # This renders no border
    cui.Container(id="example_container", style=cui.CoshStyling())
```