---
hide:
 - toc
 - navigation
 - title
---

<div style="margin-bottom: 1.5rem;" markdown>

## A UI library for Python Game-development
UI has been one of the hardest parts for Python game development. Users either have to ship their own UI tooling or use ones that are old, ugly, outdated, or too complex for the simple problem.  

CoshUI is different, it's something you add into your game loop — completely side stepping the complexity of external DSLs — and define the UI *you* want straight in Python.

</div>

---

## An Example with Pygame
CoshUI lets you build UIs that slot into any game loop easily. The highlighted code in the left-side code-block outlines all the code needed to produce the image on the right.

<div class="grid" markdown="1" style="margin-bottom: 3rem; gap: 20px;">

```python title="pygame_main.py" hl_lines="22-31"
import coshui as cui
import pygame as py

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

        with cui.CoshUIRenderer(cui.PygameBackend(screen)):
            with cui.Container(id="root_container", width=cui.FILL, height=cui.FILL, padding=20, align=cui.ALIGN_CENTER, justify=cui.JUSTIFY_CENTER, style=cui.CoshStyling(background_color=(80, 75, 255))):
                with cui.Container(id="menu_stack", direction=cui.COLUMN, gap=10, align=cui.ALIGN_CENTER):
                    cui.Label(id="title", text="CoshUI", font_size=64) 
                    cui.Button(id="start_btn", text="Start Game")
                    cui.Button(id="settings_btn", text="Settings")
                    cui.Button(id="quit_btn", text="Quit")

        if cui.get_signal("quit_btn", cui.CLICKED):
            running = False

        py.display.flip()
        clock.tick(FPS)

    py.quit()

if __name__ == "__main__":
    main()
```

![Image of menu screen produced by the code](assets/home/figure_1.png)

</div>

---


## Features
CoshUI can do quite a lot of things, from flexbox-like capabilities to animations. Here's a fraction of what is included:

<div class="grid cards" markdown>

-   :material-layers-triple:{ .lg .middle } **Backend Agnostic Architecture**
    
    ---

    CoshUI's core doesn't care about rendering the UI to the screen. It merely sets the necessary data through bundled up instructions called a `RenderContext` and sends that to the backend for rendering, making the swap between CPU-centered frameworks like `Pygame` to GPU-accelerated frameworks like `Raylib` possible.

-   :material-sync:{ .lg .middle } **State Persistence & Animation Loops**

    ---

    The library is technically immediate mode, but due to the *reconciliation layer* of CoshUI, it lets `Nodes` save their previous states, making it a sort of hybrid between immediate and retained mode. This makes it possible for **animations** to work, as all it does is slowly change the value over the specified time. 

-   :material-gesture-tap:{ .lg .middle } **Additive Signal Register**

    ---

    Unlike other UI libraries that use callbacks to determine interaction events, CoshUI takes a page out of Godot's book and implements a *signal* system. Nodes will always emit an interaction signal and users can check whether that signal is happening by accessing it through the `get_signal()` function.

-   :material-grid:{ .lg .middle } **The Box Model**

    ---

    CoshUI's user-facing API takes heavy inspiration from HTML and CSS, like determining UI structure through indentation like HTML with Python's context managers, to flexbox-like API and reusable styling from CSS. And just like them, every UI element is inherently a **box**.

</div>

To learn more, it is encouraged to start with the [tutorial](introduction/your-first-ui.md) or to read the [API.](learn-the-api/getting-started.md)

---

## Jump In

<div class="grid cards" markdown>

-   **Get Started**

    [:octicons-arrow-right-24: Installation Guide](introduction/installation.md){ data-preview }

-   **Build Your First UI**

    [:octicons-arrow-right-24: Your First UI Tutorial](introduction/your-first-ui.md){ data-preview }

-   **Read the Architecture**

    [:octicons-arrow-right-24: API Reference Docs](learn-the-api/getting-started.md){ data-preview }

-   **Check What is New**

    [:octicons-arrow-right-24: Changelog Updates](changelog.md){ data-preview }
</div>

