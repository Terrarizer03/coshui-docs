# Border Radius

### Introduction

CoshUI can let you set a `border_radius` for your `Nodes`. `border_radius` acts as the *roundness* of the corners of your `Nodes`. There are 2 ways to set `border_radius`:

```python title="Setting border_radius"
with cui.CoshUIRenderer(...):
    with cui.Container(id="example_container", style=cui.CoshStyling(border_radius=20)):
        pass
# or
with cui.CoshUIRenderer(...):
    with cui.Container(id="example_container", style=cui.CoshStyling(border_radius=(20, 20, 0, 0))):
        pass
```

When `border_radius` is given a single integer, the behavior is to apply that value to all 4 corners. When given a tuple of 4 values, it'll apply it in this order (top-left, top-right, bottom-right, and bottom-left).

### Default Value

The default value for `border_radius` is 0.

```python title="Default Behavior"
with cui.CoshUIRenderer(...):
    # This sets border_radius to 0
    with cui.Container(id="example_container", style=cui.CoshStyling()):
        pass
```