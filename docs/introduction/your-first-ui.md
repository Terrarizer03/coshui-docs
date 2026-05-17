---
hide:
 -toc
---

# Your First UI

Choose the Backend you want to follow.

### Backends

=== "Pygame"

    ## Prerequisites

    - `Python v3.10+`
    - `coshui` package
    - `pygame` dependency

    If you haven't met these requirements, please go [here](installation.md)

    ## Step By Step

    I'm guessing you've now just installed CoshUI and want to learn how to create your first UI. Well you're in luck, in CoshUI, getting started is not hard. I'll lead you through to quickly implementing your first ever UI using CoshUI.

    ### Step 1:
    **Start with creating your python file and importing `coshui` and `pygame`.**  

    ```python title="main.py" linenums="1"
    # For the sake of this tutorial, we'll be importing everything from coshui.
    from coshui import * 
    import pygame
    ```

    ### Step 2:
    **Create your constants, your main() function, initialize `pygame`, and start your main loop.**

    ```python title="main.py" linenums="5"
    WIDTH, HEIGHT = 800, 800
    FPS = 60
    BLACK = (0, 0, 0)

    def main():
        pygame.init()
        screen = pygame.display.set_mode((WIDTH, HEIGHT))
        pygame.display.set_caption("CoshUI Test")
        clock = pygame.time.Clock()

        running = True
        while running:
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    running = False
    
            screen.fill(BLACK)

            pygame.display.flip()
            clock.tick(FPS)

        pygame.quit()

    if __name__ == "__main__":
        main()
    ```

    ### Step 3:
    **Once you have the boilerplate down, it's time to create your first UI. Between `screen.fill(BLACK)` and `pygame.display.flip()`, write `with CoshUIRenderer(PygameBackend(screen))`.**

    ```python title="main.py" linenums="9" hl_lines="15-16"
    def main():
        pygame.init()
        screen = pygame.display.set_mode((WIDTH, HEIGHT))
        pygame.display.set_caption("CoshUI Test")
        clock = pygame.time.Clock()

        running = True
        while running:
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    running = False
    
            screen.fill(BLACK)

            with CoshUIRenderer(PygameBackend(screen)):
                pass

            pygame.display.flip()
            clock.tick(FPS)

        pygame.quit()
    ```

    **The `CoshUIRenderer` context is where your entire UI structure will live.**
    
    !!! warning "Multiple CoshUIRenderers"
        You **cannot** have multiple CoshUIRenderers. If you have multiple CoshUIRenderers running at once in the same loop, their layouts **WILL** overlap and UI interactions **WILL** break.

    **Now you may notice the `PygameBackend` takes in the `screen` variable, since pygame draws everything on its own `Surface` object, we pass on that surface to the backend for use.**

    ### Step 4:
    **With CoshUIRenderer down, we can finally create our UI structure. We'll start by creating a `Container` context and create a `Button` node within it.**

    ```python title="main.py" linenums="23"
        with CoshUIRenderer(PygameBackend(screen)):
            with Container(id="container_1", padding=20, style=CoshStyling(background_color=(80, 75, 255))):
                Button(id="btn", text="Click Me")
    ```

    **If you run this code, you should have a blue-ish colored container that has 20 padding with a button that says "Click Me" on the top left.**
    
    <figure markdown="span">
        ![Gif of cursor hovering and clicking the button node](../assets/introduction/step-4.gif)
    </figure>
    
    !!! note "ID Requirement"
        It is best practice to give every Node you create an `id`. Though it's not fully required, if a Node has no id, it is not **persistent** (we will get into this later).

    ### Step 5:   
    **Hopefully you've understood how CoshUI's context manager API works. With that, let's create a Start Menu with a working Quit Button and Settings Button that triggers a modal.**

    ```python title="main.py" linenums="23"
        with CoshUIRenderer(PygameBackend(screen)):
            with Container(id="container_1", width=FILL, height=FILL, style=CoshStyling(background_color=(80, 75, 255)), align=ALIGN_CENTER, justify=JUSTIFY_CENTER):
                with Container(id="main_container", direction=COLUMN, align=ALIGN_CENTER, justify=JUSTIFY_CENTER, gap=15):
                    Label(id="main_label", text="CoshUI Menu", font_size=48)
                    Button(id="settings_button", text="Settings")
                    Button(id="quit_button", text="Quit")
    ```

    **With that, we should have a decent looking Menu.**

    <figure markdown="span">
        ![image of the menu screen](../assets/introduction/tutorial-menu.png){ width=1000 }
    </figure>

    ### Step 6:
    **Now it's time to add a little bit of *interaction* to our UI. Using CoshUI's built-in interaction system, we can use the `get_signal()` function to capture events.**
    
    ```python title="main.py" linenums="23"
        with CoshUIRenderer(PygameBackend(screen)):
            with Container(id="container_1", width=FILL, height=FILL, style=CoshStyling(background_color=(80, 75, 255)), align=ALIGN_CENTER, justify=JUSTIFY_CENTER):
                with Container(id="main_container", direction=COLUMN, align=ALIGN_CENTER, justify=JUSTIFY_CENTER, gap=15):
                    Label(id="main_label", text="CoshUI Menu", font_size=48)
                    Button(id="settings_button", text="Settings")
                    Button(id="quit_button", text="Quit")

        if get_signal("quit_button", CLICKED):
            running = False
    ```

    !!! tip "Different Interactions"
        There are 6 different interactions that you can pass in for CoshUI, namely `CLICKED`, `RELEASED`, `PRESSED`, `HOVERED`, `HOVER_ENTER`, and lastly `HOVER_EXIT`. To learn more, go [here.](../learn-the-api/interactions/index.md)

    ### Step 7:
    **With our Quit Button working, we can move on to making a settings menu.**

    ```python title="main.py" linenums="5" hl_lines="4 7 31-32"
    WIDTH, HEIGHT = 800, 800
    FPS = 60
    BLACK = (0, 0, 0)
    settings_open = False

    def main():
        global settings_open
        pygame.init()
        screen = pygame.display.set_mode((WIDTH, HEIGHT))
        pygame.display.set_caption("CoshUI Test")
        clock = pygame.time.Clock()

        running = True
        while running:
            for event in pygame.event.get():
                if event.type == pygame.QUIT:
                    running = False

            screen.fill(BLACK)

            with CoshUIRenderer(PygameBackend(screen)):
                with Container(id="container_1", width=FILL, height=FILL, style=CoshStyling(background_color=(80, 75, 255)), align=ALIGN_CENTER, justify=JUSTIFY_CENTER):
                    with Container(id="main_container", direction=COLUMN, align=ALIGN_CENTER, justify=JUSTIFY_CENTER, gap=15):
                        Label(id="main_label", text="CoshUI Menu", font_size=48)
                        Button(id="settings_button", text="Settings")
                        Button(id="quit_button", text="Quit")

            if get_signal("quit_button", CLICKED):
                running = False

            if get_signal("settings_button", CLICKED):
                settings_open = not settings_open

            pygame.display.flip()
            clock.tick(FPS)

        pygame.quit()

    if __name__ == "__main__":
        main()
    ```

    **As you can see, we're toggling a boolean value whenever we click the settings button, which we can then use for conditional UI.**

    ### Step 8:
    **With our new settings_open boolean, we can add a quick if statement that opens up a modal.

    ```python title="main.py" linenums="23" hl_lines="7-16"
        with CoshUIRenderer(PygameBackend(screen)):
            with Container(id="container_1", width=FILL, height=FILL, style=CoshStyling(background_color=(80, 75, 255)), align=ALIGN_CENTER, justify=JUSTIFY_CENTER):
                with Container(id="main_container", direction=COLUMN, align=ALIGN_CENTER, justify=JUSTIFY_CENTER, gap=15):
                    Label(id="main_label", text="CoshUI Menu", font_size=48)
                    Button(id="settings_button", text="Settings")
                    Button(id="quit_button", text="Quit")
                if settings_open:
                    with Modal(id="settings_modal", width=350, height=250, direction=COLUMN, align=ALIGN_CENTER, justify=JUSTIFY_START, gap=30, padding=20):
                        Label(id="settings_title", text="Settings", height=FILL)
                        with Container(id="sfx_container", width=FILL, height=FILL, justify=JUSTIFY_SPACE_BETWEEN, direction=ROW):
                            Label(id="sfx_label", text="SFX")
                            Checkbox(id="sfx_cb")
                        with Container(id="volume_container", width=FILL, height=FILL, justify=JUSTIFY_SPACE_BETWEEN, direction=ROW):
                            Label(id="volume_label", text="Volume")
                            Slider(id="volume_slider", width=100)
                        Button(id="close_button", text="Close", height=FILL, style=CoshStyling(background_color=(255, 50, 50)))
                            
        if get_signal("quit_button", CLICKED):
            running = False

        if get_signal("settings_button", CLICKED) or get_signal("close_button", CLICKED):
            settings_open = not settings_open
    ```

=== "Raylib"

    <figure markdown="span">
        **Coming Soon...**
    </figure>

=== "PyOpenGL"

    <figure markdown="span">
        **Coming Soon...**
    </figure>