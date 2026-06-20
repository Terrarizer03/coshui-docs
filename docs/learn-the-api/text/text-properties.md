# Text Properties

### Quick Guide

| Property | Type | Default |
| :--- | :--- | :--- |
| `text` | `str` | `None` |
| `font` | `str` | `None` (uses default font) |
| `font_size` | `int` | `16` |
| `text_color` | `tuple(r, g, b)` | `(255, 255, 255)` |
| `text_align` | `CoshTextAlign` | `CENTER` |
| `text_justify` | `CoshTextJustify` | `CENTER` |
| `text_overflow` | `CoshTextOverflow` | `VISIBLE` |

### Introduction

Any `TextNode`-based Element — like `Label()` or `Button()` — exposes a set of properties to control how its text is rendered. These properties are set directly on the Node itself, not through `style`.

```python title="Basic Usage"
cui.Label(id="my_label", text="Hello, World!", font_size=20, text_color=(255, 200, 0))
```

---

### text

The string content to render.

```python title="text"
cui.Label(id="greeting", text="Welcome back!")
```

---

### font

References a font by name from CoshUI's font library, not by file path directly. CoshUI ships with `"Courier"`, `"Inter"`, and `"Ubuntu"` built in. If `font` is left as `None`, the Node falls back to the active default font.

```python title="font"
cui.Label(id="my_label", text="Styled text", font="Courier")
```

To use your own font, you first need to register it with `add_font()` before referencing it by name.

```python title="add_font()"
cui.add_font("Poppins", "assets/fonts/Poppins-Regular.ttf")

cui.Label(id="my_label", text="Custom font!", font="Poppins")
```

`add_font()` takes a name and a file path, and raises a `CoshUIError` if the path doesn't point to a valid file. Once registered, the name can be reused across any `TextNode` in your UI.

---

### font_size

Controls the pixel size of the rendered text. Defaults to `16` if not set.

```python title="font_size"
cui.Label(id="title", text="Big Title", font_size=32)
```

---

### text_color

An `(r, g, b)` tuple controlling the color of the text. Defaults to white.

```python title="text_color"
cui.Label(id="warning", text="Careful!", text_color=(255, 80, 80))
```

---

### text_align

Controls vertical alignment of the text within the Node's bounds.

| Value | Behavior |
| :--- | :--- |
| `TEXT_ALIGN_TOP` | Text is aligned to the top |
| `TEXT_ALIGN_CENTER` | Text is vertically centered |
| `TEXT_ALIGN_BOTTOM` | Text is aligned to the bottom |

```python title="text_align"
cui.Label(id="my_label", text="Top aligned", text_align=cui.TEXT_ALIGN_TOP)
```

---

### text_justify

Controls horizontal alignment of the text within the Node's bounds.

| Value | Behavior |
| :--- | :--- |
| `TEXT_JUSTIFY_LEFT` | Text is aligned to the left |
| `TEXT_JUSTIFY_CENTER` | Text is horizontally centered |
| `TEXT_JUSTIFY_RIGHT` | Text is aligned to the right |

```python title="text_justify"
cui.Label(id="my_label", text="Right aligned", text_justify=cui.TEXT_JUSTIFY_RIGHT)
```

---

### text_overflow

Controls what happens when text exceeds the Node's bounds.

| Value | Behavior |
| :--- | :--- |
| `TEXT_VISIBLE` | Text overflows the bounds without being clipped |
| `TEXT_HIDDEN` | Text is clipped at the Node's bounds |
| `TEXT_WRAP` | Text wraps onto multiple lines to fit the width |

```python title="text_overflow"
cui.Label(id="my_label", text="A long sentence that needs wrapping", width=150, text_overflow=cui.TEXT_WRAP)
```

---

### Auto Sizing

If `width` or `height` is left as `AUTO`, the Node measures the text and sizes itself to fit it exactly.

```python title="Auto Sizing"
# Sizes itself to exactly fit "Hello!" at font_size=16
cui.Label(id="auto_label", text="Hello!")
```