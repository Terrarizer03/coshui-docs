# Welcome to CoshUI 

Welcome to the documentation site of CoshUI — a **declarative** UI library built in Python **for** Python.

---

## Why CoshUI?

Before that question is answered — if you're a Python developer — I'm sure you know. Most Python UI Libraries are either old and outdated, overly complex, or both. Now before the pitchforks fly, I have to clarify that CoshUI *isn't* meant to be a replacement.  

CoshUI was made with the vision of writing minimal boilerplate but having the tools to customize it however you like. It's meant to be something you install and plug into existing projects.  

CoshUI is backend-agnostic — the same UI code works with Pygame, OpenGL, or any backend you build yourself. With its declarative API — where indentation defines hierarchy — writing UI code feels familiar if you've ever written HTML or Flutter, but in pure Python.

Now to get onto the real reason why **you** should choose CoshUI:

<figure style="text-align: center;">
    <img src="assets/home/figure_1.png" alt="CoshUI Start Menu" style="display: block; margin: 0 auto;" width=600 height=600>
    <figcaption>Figure 1. CoshUI Start Screen (Pygame)</figcaption>
</figure>

```python title="CoshUI Start Screen Code" linenums="1"
with CoshUIRenderer(PygameBackend(screen)):
    with Container(id="container_1", width=FILL, height=FILL, padding=20, style=CoshStyling(background_color=(80, 75, 255)), align=ALIGN_CENTER, justify=JUSTIFY_CENTER):
        with Container(id="container_2", direction=COLUMN, gap=10, align=ALIGN_CENTER   ):
            Label(id="label", text="CoshUI", width=100, height=100, font_size=64)
            Button(id="start_btn", text="Start")
            Button(id="settings_btn", text="Settings")
            Button(id="quit_btn", text="Quit")
```

The above image — and following code — is an example of what CoshUI can do in just a few lines. The UI in the image uses only the default themes with absolutely no styling other than `container_1`'s background color. 

---

## Introduction

[Install CoshUI Now](introduction/installation.md)  
[Learn How To Make Your First UI](introduction/your-first-ui.md)

---

## Learn the API

[Getting Started](learn-the-api/getting-started.md)

---

## Interested in Recent Updates?

[Keep Up With The Changelog](changelog.md)

---

## More Info About The Project

[Check Out The Github Repository](https://github.com/Terrarizer03/CoshUI)