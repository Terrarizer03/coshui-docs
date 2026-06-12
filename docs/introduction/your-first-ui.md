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

    ---

    ## Basic Boilerplate
    To start us off, let's make the `Pygame` boilerplate that we'll use for this tutorial. If you're following along, make sure to copy this boilerplate into your file.
    
    **Do note that all UI related code that we will be working on will be within the highlighted line.**

    ```python title="pygame_test.py" hl_lines="21"
    import pygame as py
    import coshui as cui

    WIDTH, HEIGHT = 800, 800
    FPS = 60

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

            screen.fill((0, 0, 0))

            # CoshUI Code Here

            py.display.flip()
            clock.tick(FPS)

        py.quit()

    if __name__ == "__main__":
        main()
    ```

    ---

    ## Setting Up CoshUIRenderer
    Let us move on to the *"body"* of CoshUI. `CoshUIRenderer()` is the "entry point" of the CoshUI engine, UI syntax will not work properly without it. To set it up, you must do this:
    !!! info "Highlight in Boilerplate"
        Remember to put this code within the highlighted part of the boilerplate.

    ```python title="pygame_test.py"
    with cui.CoshUIRenderer(cui.PygameBackend(screen)):
        pass
    ```

    All UI code runs within this context manager (`with` block). It registers all CoshUI nodes, determines their order of rendering, and gives you the ability to animate and interact with them for free.

    !!! note "Immediate and Retained Hybrid"
        A note to keep in mind is that CoshUI is inherently an "immediate mode" UI library, meaning it rebuilds every Node per frame. It gets away with signals and animations because it has an internal reconciliation layer that saves and sets state per frame.
    
    ### CoshUIRenderer Parameters

    Before we move on, I'd like to discuss the *parameters* `CoshUIRenderer()` takes. It takes a `CoshBackend` instance for its first parameter and a `CoshMode` instance for its second. `CoshBackend` is easy to deduce, it's the backend that we pass based on what rendering pipeline we're using, but `CoshMode` might be a little confusing.

    `CoshMode` is defaulted to `NORMAL`, which makes it run normally. But one thing you can do is set it to `DEBUG`:
    ```python title="pygame_test.py"
    with cui.CoshUIRenderer(cui.PygameBackend(screen), cui.DEBUG):
        pass
    ```

    If set to `DEBUG`, it will open up a tkinter window that lets you see the entire UI structure and click individual Nodes to see their properties for that frame (similar to DevTools on a browser). This is helpful for whenever need to check values for each Node. 

    ![image of CoshUI debugger](../assets/introduction/debugger.gif)

    ---

    ## Declaring Your First Element
    Learning new UI libraries can be scary because of the new API you have to learn, but CoshUI is built to be easy to pick up without much resistance when building or migrating the UI. If you have experience with HTML then this might seem very familiar, if you don't then that's completely okay. Let's create our first `Container` as a Node instead of a Parent. Here's how that works:

    ```python title="pygame_test.py"
    with cui.CoshUIRenderer(cui.PygameBackend(screen)):
        cui.Container(id="root_container", width=100, height=100)
    ```
    
    If you've added that to your code and ran it, you might be confused as to why nothing is showing, well no need to worry about that for now, your `Container` is currently invisible because it has no color. We'll get into styling in the next section. 
    
    Back to our example above, that `Container` instance creates a box that is 100x100 in size on the top-left of the screen. An interesting part about `Containers` is that they can actually act as context managers that take in children like this:

    ```python title="pygame_test.py"
    with cui.CoshUIRenderer(cui.PygameBackend(screen)):
        with cui.Container(id="root_container", width=100, height=100):
            cui.Container(id="child_container", width=50, height=50)
    ```
    This arrangement creates a `Container` ***within*** the `root_container` that is 50x50 in size.

    ---

    ## Styling Your First Element
    In other UI libraries, styling is mostly an afterthought. In CoshUI, styling is a primary part of the experience. To style a Node, you need to utilize CoshUI's `CoshStyling` object. It holds the properties that each Node needs to be visually distinct. To set it, you can do this:

    ```python title="pygame_test.py"
    with cui.CoshUIRenderer(cui.PygameBackend(screen)):
        cui.Container(
            id="root_container", 
            width=100, height=100, 
            style=cui.CoshStyling(background_color=(100, 100, 255))
        )
    ```
    When run, this should show your 100x100 ***light blue-ish*** `Container` at the top-left of your window. 

    ![image of blue-ish container](../assets/introduction/blue-container-pygame.gif)
    
    ### CoshStyling Parameters

    ### Reusable Styling Through *Classes*

    ---
    
    ## Layout Fundamentals
    Before moving on, let's learn a little bit about the layout properties you can set which gives you maximum control over your UI.
    
    #### Width and Height
    As shown in earlier sections, you can set width and height. These two properties are [Universal Properties](../learn-the-api/getting-started.md#definition-of-terms){ data-preview }, meaning they exist and can be set in every Node within CoshUI. They determine the size of your Node based on pixels.

    To learn more, check out the [Width and Height](../learn-the-api/layout/width-and-height.md#introduction){ data-preview } section in the API.

    #### Padding and Margin
    Margin is a [Universal Property](../learn-the-api/getting-started.md#definition-of-terms){ data-preview } whilst padding is a [Local Property](../learn-the-api/getting-started.md#definition-of-terms){ data-preview } and can only be set within `ParentNodes` (Nodes that can take in children). An example of a `ParentNode` would be `Container`. Margin is the property that dictates the space other nodes need to give around that specific Node, while padding dictates the distance the children should be from the edges of that `ParentNode`.

    To learn more, check out the [Padding and Margin](../learn-the-api/layout/padding-and-margin.md#introduction){ data-preview } section in the API.

    #### Position

    ---

=== "Raylib"

    ## Prerequisites

    - `Python v3.10+`
    - `coshui` package
    - `raylibpy` dependency

    If you haven't met these requirements, please go [here.](installation.md)

    ---

    ## Basic Boilerplate
    To start us off, let's make the `Raylib` boilerplate that we'll use for this tutorial. If you're following along, make sure to copy this boilerplate into your file.
    
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

    ---

    ## Basic Boilerplate
    To start us off, let's make the `PyOpenGL` with `GLFW` boilerplate that we'll use for this tutorial. If you're following along, make sure to copy this boilerplate into your file.
    
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

    ---

    ## Basic Boilerplate
    To start us off, let's make the `ModernGL` with `GLFW` boilerplate that we'll use for this tutorial. If you're following along, make sure to copy this boilerplate into your file.
    
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

    ---

    ## Basic Boilerplate
    To start us off, let's make the `ModernGL` with `MGLW` boilerplate that we'll use for this tutorial. If you're following along, make sure to copy this boilerplate into your file.
    
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