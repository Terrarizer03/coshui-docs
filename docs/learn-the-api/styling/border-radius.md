# Border Radius

### Quick Guide

| Property | Type | Default | Recursive or Local |
| :--- | :--- | :--- | :--- |
| `border_radius` | int **or** tuple(x, y, z, w) | 0 | Local | 

### Introduction

CoshUI can let you set a `border_radius` for your `Nodes`. `border_radius` acts as the *roundness* of the corners of your `Nodes`. There are 2 ways to set `border_radius`:

```python title="Setting border_radius"
with cui.CoshUIRenderer(...):
    cui.Container(id="example_container", style=cui.CoshStyling(border_radius=20))
# or
with cui.CoshUIRenderer(...):
    cui.Container(id="example_container", style=cui.CoshStyling(border_radius=(20, 20, 0, 0)))
```

When `border_radius` is given a single integer, the behavior is to apply that value to all 4 corners. When given a tuple of 4 values, it'll apply it in this order (top-left, top-right, bottom-right, and bottom-left).

### Default Value

The default value for `border_radius` is 0.

```python title="Default Behavior"
with cui.CoshUIRenderer(...):
    # This sets border_radius to 0
    cui.Container(id="example_container", style=cui.CoshStyling())
```