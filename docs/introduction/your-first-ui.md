---
hide:
 -toc
icon: octicons/terminal-16
---

# Your First UI

Choose the Backend you want to follow.

!!! info "Important"
    The file with the full, discussed code will be at the very end of each section.

### Backends

=== "Pygame"
    ## Prerequisites

    - `Python v3.10+`
    - `coshui` package
    - `pygame` dependency

    If you haven't met these requirements, please go [here.](installation.md)

    ## Basic Boilerplate
    To start us off, lets make the `Pygame` boilerplate that we'll use for this tutorial. 
    
    **Do note that all UI related code that we will be working on will be within the highlighted line.**

    ```python title="pygame_test.py" hl_lines="22"
    import pygame as py
    import coshui as cui

    WIDTH, HEIGHT = 800, 800
    FPS = 60
    BLACK = (0, 0, 0)

    def main():
        py.init()
        screen = py.display.set_mode((WIDTH, HEIGHT))
        py.display.set_caption("Pygame CoshUI Test")
        clock = py.time.Clock()

        running = True
        while running:
            for event in py.event.get():
                if event.type == py.QUIT:
                    running = False

            screen.fill(BLACK)

            # CoshUI Code Here

            py.display.flip()
            clock.tick(FPS)

        py.quit()

    if __name__ == "__main__":
        main()
    ```

=== "Raylib"

    ## Prerequisites

    - `Python v3.10+`
    - `coshui` package
    - `raylibpy` dependency

    If you haven't met these requirements, please go [here.](installation.md)

    ## Basic Boilerplate
    To start us off, lets make the `Raylib` boilerplate that we'll use for this tutorial. 
    
    **Do note that all UI related code that we will be working on will be within the highlighted line.**

    ```python title="raylib_test.py" hl_lines="15"
    import raylibpy as rl
    import coshui as cui

    WIDTH, HEIGHT = 800, 800
    FPS = 60

    def main():
        rl.init_window(WIDTH, HEIGHT, "Raylib CoshUI Test")
        rl.set_target_fps(FPS)

        while not rl.window_should_close():
            rl.begin_drawing()
            rl.clear_background(rl.BLACK)
            
            # CoshUI Code Here

            rl.end_drawing()

        rl.close_window()

    if __name__ == "__main__":
        main()
    ```

=== "PyOpenGL | GLFW"

    ## Prerequisites

    - `Python v3.10+`
    - `coshui` package
    - `PyOpenGL` dependency
    - `PyOpenGL_accelerate` dependency (this is optional)

    If you haven't met these requirements, please go [here.](installation.md)

    ## Basic Boilerplate
    To start us off, lets make the `PyOpenGL` with `GLFW` boilerplate that we'll use for this tutorial. 
    
    **Do note that all UI related code that we will be working on will be within the highlighted line.**

    ```python title="pyopengl_glfw_test.py" hl_lines="20"
    import glfw
    from OpenGL.GL import *
    import coshui as cui

    def main():
        if not glfw.init(): return

        window = glfw.create_window(800, 800, "PyOpenGL::GLFW CoshUI Test", None, None)
        if not window:
            glfw.terminate()
            return

        glfw.make_context_current(window)

        glClearColor(0.0, 0.0, 0.0, 1.0)

        while not glfw.window_should_close(window):
            glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT)

            # CoshUI Code Here

            glfw.swap_buffers(window)
            glfw.poll_events()

        glfw.terminate()

    if __name__ == "__main__":
        main()
    ```

=== "ModernGL | GLFW"

    ## Prerequisites

    - `Python v3.10+`
    - `coshui` package
    - `moderngl` dependency

    If you haven't met these requirements, please go [here.](installation.md)

    ## Basic Boilerplate
    To start us off, lets make the `ModernGL` with `GLFW` boilerplate that we'll use for this tutorial. 
    
    **Do note that all UI related code that we will be working on will be within the highlighted line.**

    ```python title="moderngl_glfw_test.py" hl_lines="20"
    import moderngl
    import glfw
    import coshui as cui    

    def main():
        if not glfw.init(): return

        window = glfw.create_window(800, 800, "ModernGL::GLFW CoshUI Test", None, None)
        if not window:
            glfw.terminate()
            return

        glfw.make_context_current(window)

        ctx = moderngl.create_context()

        while not glfw.window_should_close(window):
            ctx.clear(0.0, 0.0, 0.0, 1.0)

            # CoshUI Code Here

            glfw.swap_buffers(window)
            glfw.poll_events()

        glfw.terminate()

    if __name__ == "__main__":
        main()
    ```

=== "ModernGL | MGLW"

    ## Prerequisites

    - `Python v3.10+`
    - `coshui` package
    - `moderngl` dependency
    - `moderngl-window` dependency

    If you haven't met these requirements, please go [here.](installation.md)

    ## Basic Boilerplate
    To start us off, lets make the `ModernGL` with `MGLW` boilerplate that we'll use for this tutorial. 
    
    **Do note that all UI related code that we will be working on will be within the highlighted line.**

    !!! warning "ModernGL Window"
        CoshUI works somewhat *weirdly* with ModernGL Window. Due to ModernGL Window's architecture being mostly enclosed, developing a work around for using the library has been incredibly tough. CoshUI has to utilize internal functions — as shown in the `on_mouse_position_event()` method where we set the internal `_mouse_pos` member variable — just to make the interaction system work. If you're using MGLW, be warned that although it works, CoshUI might have some future *issues* with the arrangement.

    ```python title="moderngl_mglw_test.py" hl_lines="19"
    import moderngl_window as mglw
    import coshui as cui

    class MyRenderer(mglw.WindowConfig):
        gl_version = (3, 3)
        title = "ModernGL::MGLW CoshUI Test"
        window_size = (800, 800)
        aspect_ratio = 16 / 9
        resizable = True

        def __init__(self, **kwargs):
            super().__init__(**kwargs)
            self.mouse_x = 0
            self.mouse_y = 0

        def on_render(self, time: float, frametime: float):
            self.ctx.clear(0.1, 0.1, 0.1)

            # CoshUI Code Here

        def on_resize(self, width: int, height: int):
            self.ctx.viewport = (0, 0, width, height)

        def on_mouse_position_event(self, x, y, dx, dy):
            self.mouse_x = x
            self.mouse_y = y

            # NOTE: This `on_mouse_position_event` method and this _mouse_pos = (x, y) is
            # necessary for CoshUI's interaction system to work. 
            mglw.window()._mouse_pos = (x, y)

    if __name__ == '__main__':
        mglw.run_window_config(MyRenderer)
    ```