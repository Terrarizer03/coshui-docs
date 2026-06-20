# Properties

### Quick Guide

| Property | Type | Description |
| :--- | :--- | :--- |
| `alpha` | `float` | Opacity of the Node |
| `background_color` | `tuple(r, g, b)` | Background color of the Node |
| `transform_position` | `tuple(x, y)` | Positional offset applied at render time |
| `transform_scale` | `float` | Scale multiplier applied at render time |
| `transform_rotation` | `float` | Rotation in degrees applied at render time |

### Introduction

Not every Node property can be animated — only properties that are tracked in state and interpolated by the tween system are supported. These are primarily the visual and transform properties that make the most sense to animate.

---

### alpha

Animates the opacity of a Node. Expects a `float` between `0` and `255`, where `0` is fully transparent and `255` is fully opaque.

```python title="Alpha"
# Fade out
cui.animate("alpha", "my_panel", 0, 0.5, "ease_in")

# Fade in
cui.animate("alpha", "my_panel", 255, 0.5, "ease_out")
```

---

### background_color

Animates the background color of a Node. Expects an `(r, g, b)` tuple with values between `0` and `255`.

```python title="background_color"
cui.animate("background_color", "my_btn", (255, 80, 80), 0.2, "ease_out")
```

Note that `Checkbox` does not support `background_color` animation since its color directly represents its checked state.

---

### transform_position

Animates a positional offset applied on top of the Node's laid-out position. Expects an `(x, y)` tuple. This does not affect layout — it's a visual offset only, applied at render time.

```python title="transform_position"
# Slide down by 20px
cui.animate("transform_position", "my_panel", (0, 20), 0.3, "ease_out")
```

---

### transform_scale

Animates the scale of a Node around its center. Expects a `float`, where `1.0` is the original size.

```python title="transform_scale"
# Grow slightly on hover
if cui.get_signal("my_card", cui.HOVER_ENTER):
    cui.animate("transform_scale", "my_card", 1.05, 0.15, "ease_out")

if cui.get_signal("my_card", cui.HOVER_EXIT):
    cui.animate("transform_scale", "my_card", 1.0, 0.15, "ease_out")
```

---

### transform_rotation

Animates the rotation of a Node around its center. Expects a `float` in degrees.

```python title="transform_rotation"
cui.animate("transform_rotation", "my_icon", 180.0, 0.4, "ease_in_out")
```