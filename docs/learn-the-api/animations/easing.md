# Easing

### Quick Guide

| Easing | Description |
| :--- | :--- |
| `linear` | Constant speed throughout |
| `ease_in` | Starts slow, ends fast |
| `ease_out` | Starts fast, ends slow |
| `ease_in_out` | Starts slow, speeds up, ends slow |
| `ease_in_bounce` | Bounces at the start before moving |
| `ease_out_bounce` | Bounces at the end before settling |
| `ease_in_elastic` | Overshoots backward at the start like a rubber band |
| `ease_out_elastic` | Overshoots forward at the end like a rubber band |

### Introduction

Easing curves control how an animation progresses over its duration. Without easing, animations feel mechanical and robotic. With the right curve, they feel alive. You pass the easing curve as a string to `animate()`.

```python title="Basic Usage"
cui.animate("background_color", "my_btn", (255, 0, 0), 0.3, "ease_out")
```

### linear

Progresses at a constant rate from start to finish. Rarely the best choice for UI but useful when you want something purely mechanical or when animating something like a progress bar.

```python title="linear"
cui.animate("alpha", "my_bar", 255, 1.0, "linear")
```

### ease_in

Starts slow and accelerates toward the end. Good for elements that are leaving the screen — they build up speed as they exit.

```python title="ease_in"
cui.animate("alpha", "my_panel", 0, 0.3, "ease_in")
```

### ease_out

Starts fast and decelerates toward the end. Good for elements entering the screen — they arrive quickly and settle into place.

```python title="ease_out"
cui.animate("transform_position", "my_panel", (0, 0), 0.3, "ease_out")
```

### ease_in_out

Starts slow, speeds up in the middle, and slows down again at the end. A safe, natural-feeling default for most UI transitions.

```python title="ease_in_out"
cui.animate("transform_scale", "my_modal", 1.0, 0.4, "ease_in_out")
```

### ease_out_bounce

Overshoots the target value at the end and bounces back to settle. Good for playful UI elements like notifications or popups appearing.

```python title="ease_out_bounce"
cui.animate("transform_scale", "my_toast", 1.0, 0.5, "ease_out_bounce")
```

### ease_in_bounce

Bounces at the start before committing to the animation. Less commonly used but good for elements that need a windup feel before exiting.

```python title="ease_in_bounce"
cui.animate("transform_position", "my_panel", (0, 500), 0.5, "ease_in_bounce")
```

### ease_out_elastic

Overshoots the target and snaps back like a rubber band. Great for interactive elements like buttons or toggles that need to feel springy and responsive.

```python title="ease_out_elastic"
if cui.get_signal("my_btn", cui.CLICKED):
    cui.animate("transform_scale", "my_btn", 1.0, 0.4, "ease_out_elastic")
```

### ease_in_elastic

Pulls back in the opposite direction before launching toward the target. Useful for dramatic exits or attention-grabbing transitions.

```python title="ease_in_elastic"
cui.animate("transform_position", "my_panel", (600, 0), 0.5, "ease_in_elastic")
```