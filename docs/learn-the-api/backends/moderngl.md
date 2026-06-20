# ModernGL

### Quick Guide

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `context` | `moderngl.Context` | The active ModernGL graphics context |
| `driver` | `cui.Windower` | Either `cui.GLFW` or `cui.MGLW` |

### Introduction

`ModernGLBackend` is CoshUI's backend for raw OpenGL rendering via [ModernGL](https://github.com/moderngl/moderngl). Unlike `PygameBackend` or `RaylibBackend`, ModernGL isn't a full game framework — it's a thin wrapper around OpenGL itself — which means CoshUI needs to know both the graphics context to render into *and* which windowing system is supplying input and window size. That's where the `Windower` comes in.

=== "GLFW"

    ```python title="Setup with GLFW"
    import moderngl
    import glfw
    import coshui as cui

    glfw.init()
    window = glfw.create_window(800, 600, "My App", None, None)
    glfw.make_context_current(window)
    context = moderngl.create_context()

    # Created once, outside the loop, since shader compilation is expensive
    backend = cui.ModernGLBackend(context, cui.GLFW)

    while not glfw.window_should_close(window):
        glfw.poll_events()

        with cui.CoshUIRenderer(backend):
            cui.Label(id="hello", text="Hello, ModernGL!")

        glfw.swap_buffers(window)
    ```

=== "MGLW"

    ```python title="Setup with moderngl-window"
    ...

    def __init__(self):
        ...
        
        self.coshui_backend = cui.ModernGLBackend(self.ctx, cui.MGLW)

    def on_render(self, time, frametime):
        ...

        with cui.CoshUIRenderer(self.coshui_backend):
            cui.Label(id="hello", text="Hello, ModernGL!")
    ```

It's important to construct `ModernGLBackend` **once**, outside your render loop, since its constructor compiles all of CoshUI's shaders (rect, text, and image) up front. Recreating it every frame would mean recompiling every shader every frame.

---

### Windowers

CoshUI supports two windowers for ModernGL: `cui.GLFW` and `cui.MGLW` (moderngl-window). The windower is responsible for two things — reporting the window size via `_get_size()`, and polling mouse input via `_poll_input()` — both of which CoshUI calls automatically every frame.

!!! warning "MGLW Input Caveat"
    The `MGLW` driver reads mouse position from `moderngl_window.window()._mouse_pos`, which moderngl-window only populates if you've already wired up mouse movement tracking yourself (typically by calling `_calc_mouse_delta()` or setting `_mouse_pos` in your own `on_mouse_position_event`). If you're seeing no mouse interaction with `MGLW`, this is almost always why.

---

### How Rendering Works

`ModernGLBackend.flush()` walks the render stack and dispatches each `RenderContext` to `_draw_rect`, `_draw_text`, or `_draw_image`. Each of these uploads a small quad (6 vertices, 2 triangles) to a reusable vertex buffer and draws it using a dedicated shader program for that draw type.

---

### Rects and Borders

Rect drawing uses a signed-distance-field (SDF) approach in `rect.frag`, which computes whether each pixel falls inside the rounded rect shape, the border ring, or outside entirely — entirely on the GPU. This is what allows asymmetric border radii and anti-aliased rounded corners without needing a CPU-side fallback like `RaylibBackend` does. Border radius values are clamped to half the rect's smallest dimension to avoid visual artifacts on small Nodes with large radii.

---

### Text

Text rendering uses a glyph atlas system (`gl_font.py`) built with `freetype-py`. Each unique `(font_path, font_size)` combination generates a 512x512 texture atlas containing the printable ASCII glyph set, which is then cached and reused. Glyph quads are batched into a single vertex buffer per line and drawn in one draw call. The text shader (`text.frag`) samples the alpha channel of the atlas texture to render anti-aliased glyph edges.

---

### Images

Images are loaded via Pillow (`PIL.Image`) and uploaded as a texture once, then cached by file path. They're drawn as a textured quad using the image shader.

---

### Clipping

Clipping uses OpenGL's scissor test (`context.scissor`), converting CoshUI's clip rect from top-left-origin screen coordinates into OpenGL's bottom-left-origin scissor coordinates.

---

### Input Polling

Input polling is delegated entirely to the chosen `Windower` driver. `ModernGLBackend.poll_input()` simply calls `self.driver._poll_input()`, which updates `CoshInput`'s mouse position, delta, and pressed state based on whichever windowing library is active.