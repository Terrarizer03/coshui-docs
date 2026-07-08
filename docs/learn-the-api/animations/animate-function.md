# Animate Function

### Quick Guide

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `n_property` | `str` | The property to animate |
| `target_id` | `str` | The `id` of the Node to animate |
| `end_value` | `float | tuple` | The target value to animate to |
| `duration` | `float` | Duration of the animation in seconds |
| `easing` | `str` | The easing curve to use |

### Introduction

`animate()` is how you drive animations in CoshUI. You give it a property, a Node id, a target value, a duration, and an easing curve — and CoshUI handles the rest, interpolating the value every frame until it reaches the target.

```python title="Basic Usage"
cui.animate("background_color", "my_btn", (255, 0, 0), 0.3, "ease_in_out")
```

This animates `my_btn`'s background color to red over 0.3 seconds using the `ease_in_out` curve.

---

### How It Works

`animate()` creates a `Tween` internally and registers it to the global tween registry. Each frame, every active `Tween` updates its target Node's value in `_state_storage` via `set_state`, which then gets picked up by the reconciler the next time that Node is initialized.

This means animations persist across frames automatically — you don't need to call `animate()` every frame, just once to kick it off.

```python title="Triggering on Hover"
with cui.CoshUIRenderer(...):
    cui.Button(id="my_btn", text="Hover Me")

    if cui.get_signal("my_btn", cui.HOVER_ENTER):
        cui.animate("background_color", "my_btn", (255, 100, 0), 0.2, "ease_out")

    if cui.get_signal("my_btn", cui.HOVER_EXIT):
        cui.animate("background_color", "my_btn", (86, 115, 143), 0.2, "ease_out")
```

---

### Interrupting Animations

If you call `animate()` on a property that is already being animated on the same Node, CoshUI cancels the existing tween and starts the new one. This means you don't need to manually stop anything — just call `animate()` again with the new target.

```python title="Interrupting"
# If this fires while a previous color animation is running, it takes over cleanly
if cui.get_signal("my_btn", cui.CLICKED):
    cui.animate("background_color", "my_btn", (255, 255, 255), 0.1, "ease_in")
```

---

### On Complete Callback

`animate()` returns the `Tween` it creates, which exposes a `.finished()` method for running a callback once the animation completes.

```python title="On Complete"
cui.animate("alpha", "my_panel", 0, 0.3, "ease_in").finished(lambda: print("Faded out!"))
```

---

### Loop Method

Another method `Tween` has is the `.loop()` method. Obvious is obvious, but it lets you loop your animations without needing to chain `.finished()` calls.

It accepts 3 parameters, in this order — `count`, `ping_pong`, `delay`:

- `count`: The total number of times the animation will play through, including the first. `None` (the default) means infinite.
- `ping_pong`: A boolean. If `True`, each loop reverses direction — smoothly animating back from the end value to the start value instead of jumping back to the start. If `False` (default), each loop restarts from the original start value in the same direction.
- `delay`: How long to pause between iterations, in seconds. Defaults to `0.0` (no pause).

```python title="Loop"
cui.animate("alpha", "my_panel", 0, 0.3, "ease_in").loop(count=None, ping_pong=True, delay=0.5)
```

---

### Default Behavior

If an invalid property, Node id, or easing curve is passed, CoshUI raises a `CoshUIError` with a suggestion for what you might have meant.