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
| `bold` | `bool` | `False` |
| `italic`  | `bool` | `False` |
| `strikethrough`  | `bool` | `False` |
| `underline`  | `bool` | `False` |


### Introduction

Any `TextNode`-based Element — like `Label()` or `Button()` — exposes a set of properties to control how its text is rendered. These properties are set directly on the Node itself, not through `style`, and act as the default style for the whole string.

```python title="Basic Usage"
cui.Label(id="my_label", text="Hello, World!", font_size=20, text_color=(255, 200, 0))
```

`RichLabel` shares these same base properties, but also parses CoshML tags inside `text` to override styling for specific portions of the string — see [CoshML](coshml.md) for that.

---

### text

The string content to render.

```python title="text"
cui.Label(id="greeting", text="Welcome back!")
```

---

### font

References a font by name from CoshUI's font library, not by file path directly. If `font` is left as `None`, the Node falls back to the active default font. See [Fonts](fonts.md) for registering your own.

```python title="font"
# Courier is one of the 3 fonts that comes with CoshUI
cui.Label(id="my_label", text="Styled text", font="Courier")
```

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

### bold and italic

These properties require you to add extra font paths for that specific font family when calling `add_font()`. This is discussed in the [Fonts](fonts.md) section.

The `bold` property is boolean value that sets whether the text uses the bold font path.

```python title="bold"
cui.Label(id="warning", text="Bold Text!", bold=True)
```

Whilst the `italic` property is a boolean value that sets whether the text uses the italic font path.

```python title="italic"
cui.Label(id="warning", text="Italic Text!", italic=True)
```

!!! note "bold AND italic"
    Both bold and italic booleans can be set to `True` if you've passed in a `bold_italic` font path for that font family.  
    ```python title="bold and italic"
    cui.Label(id="warning", text="Bold Text!", bold=True, italic=True)
    ```

---

### strikethrough

A boolean value that sets whether the text has a strike line through it.

```python title="strikethrough"
cui.Label(id="warning", text="This text has strikethrough.", strikethrough=True)
```

---

### underline

A boolean value that sets whether the text has an underline below it.

```python title="underline"
cui.Label(id="warning", text="This text has an underline.", underline=True)
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