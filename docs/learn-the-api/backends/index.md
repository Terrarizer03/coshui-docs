# Overview

Welcome to the backends section, as stated multiple times in this docs page, CoshUI is *backend-aagnostic* which lets users render the same UI code in different game frameworks. In the current **version {{ version }}**, there are *4 backends* for us to use. `PygameBackend`, `RaylibBackend`, `ModernGLBackend` (with `GLFW` and `MGLW` support), and `PyOpenGLBackend` (with `GLFW` support).

## Pygame

For the `PygameBackend`, it takes in a `pygame.Surface` object as the parameter as pygame draws using surfaces. To invoke a `PygameBackend`, set this in your `CoshUIRenderer`:

```python
# screen is the pygame.Surface
with CoshUIRenderer(PygameBackend(screen)):
    pass
```

To learn more about how `Nodes` are rendered in pygame or just want to learn deeply about how CoshUI wraps its draw calls, [click here.](pygame.md)

## Raylib

For the `RaylibBackend` — unlike pygame — it draws on the active display, thus not needing to input a parameter. Which in more ways than one is much more helpful for migration. To invoke a `RaylibBackend`, set this in your `CoshUIRenderer`:

```python
with CoshUIRenderer(RaylibBackend()):
    pass
```

To learn more about how `Nodes` are rendered in raylibpy or just want to learn deeply about how CoshUI wraps its draw calls, [click here.](raylib.md)

## ModernGL

For the `ModernGLBackend`, it takes in a `moderngl.Context` object and a `cui.Windower`, since it is basically the raw graphics renderer, it becomes a little different from the backends before it that are frameworks. CoshUI supports **2** *windowers* for ModernGL, `GLFW` and `moderngl-window`. To create a `ModernGLBackend`, set this in `CoshUIRenderer`:

```python
# This is set outside the loop so shader compiling is initialized only once
backend = cui.ModernGLBackend(context, cui.GLFW) 
# or 
self.backend = cui.ModernGLBackend(self.ctx, cui.MGLW) 

# Within the main render loop
with CoshUIRenderer(backend): # or self.backend
    pass
```

To learn more about how ModernGL deals with rendering `Nodes` and how different windowers works, [click here.](moderngl.md)

## PyOpenGL

For `PyOpenGLBackend` — similar to `ModernGLBackend` — it is a graphics renderer, which means it *similarly* takes in a windower, but differently, it doesn't need the current context since PyOpenGL automatically uses the active context. CoshUI supports only `GLFW` for PyOpenGL. To create a `PyOpenGLBackend`, set this in `CoshUIRenderer`:   

```python
# Again set outside the loop so shader compiling is initialized only once
backend = cui.PyOpenGLBackend(cui.GLFW) 

# Within the main render loop
with CoshUIRenderer(backend):
    pass
```

To lear more deeply about how PyOpenGL renders `Nodes` or how the windowers work, [click here.](pyopengl.md)