# Pygame

### Quick Guide

| Parameter | Type | Description |
| :--- | :--- | :--- |
| `surface` | `pygame.Surface` | The Pygame surface CoshUI draws onto |

### Introduction

`PygameBackend` is CoshUI's backend for [Pygame](https://www.pygame.org/), and is likely the easiest backend to get started with since it doesn't require any windower setup or graphics context management — Pygame handles all of that for you already.

```python title="Setup"
import pygame
import coshui as cui

pygame.init()
screen = pygame.display.set_mode((800, 600))

while running:
    with cui.CoshUIRenderer(cui.PygameBackend(screen)):
        cui.Label(id="hello", text="Hello, Pygame!")

    pygame.display.flip()
```

Since Pygame draws onto a `Surface` rather than a graphics context, `PygameBackend` takes that `Surface` directly as its only constructor parameter. CoshUI uses it for all of its draw calls.

---

### How Rendering Works

Every Node CoshUI renders eventually becomes a `RenderContext` — a flattened, render-ready snapshot of that Node's visual data (position, size, color, border, alpha, and so on). `PygameBackend.flush()` iterates over the full render stack and dispatches each `RenderContext` to one of three internal draw calls: `_draw_rect`, `_draw_text`, or `_draw_image`, depending on whether the Node has a `background_color`, `text`, or `image_src` set.

---

### Rects and Borders

Rectangles are drawn using `pygame.draw.rect()`, with `border_radius` mapped onto Pygame's per-corner radius parameters. If a Node has `alpha < 255` or a non-zero `transform_rotation`, CoshUI draws onto a temporary `SRCALPHA` surface first so that transparency and rotation composite correctly, then blits that surface onto the main one. Without that step, Pygame's native rect drawing doesn't support partial transparency or rotation directly.

---

### Text

Text rendering goes through `pygame.font.Font`, with fonts cached by `(font_path, font_size)` so the same font isn't reloaded every frame. Word-wrapping for `TEXT_WRAP` is handled manually by CoshUI, measuring word-by-word with `font.size()` until a line would exceed the Node's width. Rotated text is rendered the same way as rects — onto an intermediate surface that's rotated and re-blitted, recentered so rotation pivots around the text's own center.

---

### Images

Images are loaded with `pygame.image.load()` and cached by file path so each image is only ever loaded from disk once. They're scaled to the Node's resolved width and height using `pygame.transform.smoothscale()` every frame.

---

### Clipping

Overflow clipping (for `CoshOverflow.HIDDEN` containers and `TEXT_HIDDEN`/`TEXT_WRAP` text) is implemented using `surface.set_clip()`, which Pygame resets to `None` after each draw call to avoid leaking the clip rect into unrelated draws.

---

### Input Polling

`PygameBackend.poll_input()` reads `pygame.mouse.get_pos()` and `pygame.mouse.get_rel()` for position and delta, and `pygame.mouse.get_pressed()[0]` for the left mouse button state. This is called automatically once per frame inside `CoshUIRenderer.__enter__()` — you don't need to call it yourself.

---

### Measuring Text

`measure_text()` is used internally during the measure pass to determine `AUTO`-sized text dimensions. It uses the same cached `pygame.font.Font` objects as `_draw_text`, calling `font.size(text)` to get pixel dimensions.