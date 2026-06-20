# PyOpenGL

### Quick Guide

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `driver` | `cui.Windower` | Currently only `cui.GLFW` is supported |

### Introduction

`PyOpenGLBackend` is CoshUI's backend for raw OpenGL rendering via [PyOpenGL](http://pyopengl.sourceforge.net/), and serves as an alternative to `ModernGLBackend` for projects that prefer PyOpenGL's more direct, classic OpenGL-style API over ModernGL's higher-level wrapper.

```python title="Setup"
import glfw
import coshui as cui

glfw.init()
window = glfw.create_window(800, 600, "My App", None, None)
glfw.make_context_current(window)

# Created once, outside the loop, since shader compilation is expensive
backend = cui.PyOpenGLBackend(cui.GLFW)

while not glfw.window_should_close(window):
    glfw.poll_events()
    with cui.CoshUIRenderer(backend):
        cui.Label(id="hello", text="Hello, PyOpenGL!")
    glfw.swap_buffers(window)
```

Unlike `ModernGLBackend`, `PyOpenGLBackend` doesn't take a context object as a parameter. PyOpenGL operates directly on whichever OpenGL context is currently active on the calling thread, so as long as `glfw.make_context_current()` (or equivalent) has been called beforehand, PyOpenGL will use it automatically.

As with `ModernGLBackend`, construct `PyOpenGLBackend` **once** outside your render loop — its constructor compiles and links all of CoshUI's shaders, and doing that every frame would be wasteful and slow.

---

### Windowers

Currently, `PyOpenGLBackend` only supports `cui.GLFW` as a windower. The `GLFW` driver handles reporting window size and polling mouse input, both called automatically by CoshUI each frame — you don't need to call these yourself.

---

### How Rendering Works

`PyOpenGLBackend.flush()` walks the render stack and dispatches each `RenderContext` to `_draw_rect`, `_draw_text`, or `_draw_image`, mirroring `ModernGLBackend`'s structure closely but using PyOpenGL's lower-level, function-based API (`glGenBuffers`, `glBufferData`, `glDrawArrays`, and so on) instead of ModernGL's object-oriented wrappers.

---

### Rects and Borders

Like `ModernGLBackend`, rects are drawn using the same SDF-based `rect.frag` shader, giving anti-aliased rounded corners and asymmetric border radii support entirely on the GPU. The vertex and fragment shader source files are shared between both GL backends.

---

### Text

Text rendering uses the same glyph atlas system as `ModernGLBackend` (`gl_font.py`), generating a 512x512 texture atlas per unique `(font_path, font_size)` pair using `freetype-py`. The key difference is purely in how the texture and buffers are created and bound — using raw `glGenTextures`/`glTexImage2D` calls instead of ModernGL's `context.texture()` wrapper.

---

### Images

Images are loaded with Pillow and uploaded via `glTexImage2D`, cached by file path so repeated draws of the same image don't re-upload the texture.

---

### Clipping

Clipping uses the OpenGL scissor test via `glScissor()`, with the same top-left-to-bottom-left coordinate flip as `ModernGLBackend` to account for OpenGL's coordinate system.

---

### Input Polling

`PyOpenGLBackend.poll_input()` delegates to `self.driver._poll_input()`, same as `ModernGLBackend`. Since only `GLFW` is supported here, input is always read via `glfw.get_cursor_pos()` and `glfw.get_mouse_button()`.