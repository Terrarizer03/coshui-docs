# Transforms

### Quick Guide

| Property | Type | Default | Recursive or Local |
| :--- | :--- | :--- | :--- |
| `transform_position` | tuple(x, y) | (0, 0) | Recursive | 
| `transform_scale` | float | 1.0 | Local |
| `transform_rotation` | float | 0.0 | Local |

### Introduction

In CoshUI, there are styling properties that are considered "transform" properties. These are attributes that only alter the **rendering** side of the UI Engine without touching the layout pipeline. 

In version {{ version }}, there are 3 "transform" properties:  

- `transform_position` 
- `transform_scale`
- `transform_rotation`

---

### `transform_position` 

Let's start with `transform_position`, this property is a property that lets you *move* `Nodes` without needing to sacrifice its `RELATIVE` positioning. It takes in a 2-value `tuple` that describes the **x** and **y** offset.  

```python title="Setting transform_position"
with cui.CoshUIRenderer(...):
    with cui.Container(id="example_container", style=cui.CoshStyling(transform_position=(50, 50))):
        pass
```

The code-block above offsets the current *rendered* position of the `Node` by 50 pixels in the x direction and 50 pixels in the y direction. The layout calculations are unaffected, the true `x` and `y` values of a `Node` don't change, but the rendering is just *offset* by those transform values. 

---

### `transform_scale`

Moving on, `transform_scale` is the property that changes the scale of the `Node`. The parameter takes in a float or integer that multiplies the current `width` and `height` values when **rendering**.

```python title="Setting transform_scale"
with cui.CoshUIRenderer(...):
    with cui.Container(id="example_container", style=cui.CoshStyling(transform_scale=2.5)):
        pass
```

This code-block makes the Container **2.5 times** bigger in scale with — again — the layout pipeline's calculations being unaffected.

---

### `transform_rotation`

Finally, we get to `transform_rotation`, a property that changes the nodes *rotation*. It takes in a degree in float-form.

```python title="Setting transform_rotation"
with cui.CoshUIRenderer(...):
    with cui.Container(id="example_container", style=cui.CoshStyling(transform_rotation=45.0)):
        pass
```

The code block sets the `transform_rotation` property on the `Node` object with a 45.0 degree tilt.

---

### Default Behavior

For `transform_position`, the default behavior for the engine is to set it to (0, 0) offset if unset by the user. For `transform_scale`, the default behavior is for the engine to set it to 1.0 if user doesn't explicitly set. And for `transform_rotation`, it is set to 0.0 by the engine if not explicitly set by the user.

```python title="Default Behavior"
with cui.CoshUIRenderer(...):
    # transform_position = (0, 0)
    # transform_scale = 1.0
    # transform_rotation = 0.0
    with cui.Container(id="example_container", style=cui.CoshStyling()):
```

!!! note "Recursive or Local"
    These values are **local values**, they live only on the `Node` they are set on and do not propagate to their children **EXCEPT** for `transform_position`. In the current version of {{ version }}, there are active discussions to turn all "transform" properties to **recursive values**.