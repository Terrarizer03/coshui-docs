# Raylib

### Quick Guide

| Parameter | Type | Description |
| :--- | :--- | :--- |
| *(none)* | — | `RaylibBackend()` takes no parameters |

### Introduction

`RaylibBackend` is CoshUI's backend for [raylibpy](https://github.com/overdev/raylib-py). Unlike `PygameBackend`, it doesn't draw onto an explicit surface object — raylib always draws to the currently active window — so `RaylibBackend()` takes no constructor parameters at all.

```python title="Setup"
import raylibpy
import coshui as cui

raylibpy.init_window(800, 600, "My App")

while not raylibpy.window_should_close():
    raylibpy.begin_drawing()
    raylibpy.clear_background(raylibpy.RAYWHITE)

    with cui.CoshUIRenderer(cui.RaylibBackend()):
        cui.Label(id="hello", text="Hello, raylib!")

    raylibpy.end_drawing()
```

This makes `RaylibBackend` the most drop-in friendly backend if you're migrating an existing raylib project — there's no context or surface plumbing required beyond making sure the window is already initialized.

---

### How Rendering Works

Like every other backend, `RaylibBackend.flush()` walks the render stack produced by CoshUI's render pass and dispatches each `RenderContext` to `_draw_rect`, `_draw_text`, or `_draw_image` based on which visual properties are set.

---

### Rects and Borders

For rects with a uniform `border_radius` (all four corners equal), CoshUI uses raylib's native `draw_rectangle_rounded()` and `draw_rectangle_rounded_lines_ex()` for the fill and border respectively, since raylib only supports a single uniform roundness value out of the box. If `border_radius` is *asymmetric* (different per corner), CoshUI falls back to a custom implementation (`_draw_asymmetric_rect`) that manually draws each rounded corner as a circle sector alongside straight rectangle segments, since raylib has no native support for independently-radiused corners.

Rotation is handled using raylib's matrix stack — `rl_push_matrix()`, `rl_translatef()`, and `rl_rotatef()` are used to rotate around the rect's center before drawing, then popped back afterward.

---

### Text

Fonts are loaded with `load_font_ex()` at a fixed internal resolution of 128px and then scaled at draw time, which keeps text looking sharp across different `font_size` values without needing to reload separate font assets. Fonts are cached by path so they're only loaded once. Word-wrapping is handled the same way as the other backends — manually measuring with `measure_text_ex()` word-by-word. Rotated text uses `draw_text_pro()` with an origin set to the text's own center so it rotates in place.

---

### Images

Images are loaded with `load_texture()` and cached by path. They're drawn using `draw_texture_pro()`, which lets CoshUI scale, position, and rotate the texture in a single call without needing a separate transform step like the other backends require.

---

### Clipping

Clipping uses raylib's scissor mode via `begin_scissor_mode()` / `end_scissor_mode()`, which is raylib's native equivalent to a clip rect.

---

### Input Polling

`RaylibBackend.poll_input()` reads `get_mouse_position()` and `get_mouse_delta()` for position and delta, and `is_mouse_button_down(MOUSE_BUTTON_LEFT)` for the left mouse button. Like the other backends, this is called automatically each frame and doesn't need to be invoked manually.