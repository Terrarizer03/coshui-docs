# Borders

### Introduction

Borders in CoshUI act as the *outline* of rectangles. When setting a border, it naturally takes in the `color` of that border and the `weight`. You can set it in 2 ways, like this:

```python title="Setting border"
with cui.CoshUIRenderer(...):
    with cui.Container(id="example_container", style=cui.CoshStyling(border=((255, 0, 0), 5))):
        pass
# or
with cui.CoshUIRenderer(...):
    with cui.Container(id="example_container", style=cui.CoshStyling(border=(255, 0, 0, 5))):
        pass
```

The border that's set above will be a <span style="color: #ff0000;">red</span> border with 5 weight.

### Default Behavior

The default behavior of `border` is `None`.

```python title="Setting border"
with cui.CoshUIRenderer(...):
    # This renders no border
    with cui.Container(id="example_container", style=cui.CoshStyling()):
        pass
```