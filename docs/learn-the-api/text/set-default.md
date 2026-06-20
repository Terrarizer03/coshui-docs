# Set Default Font

### Quick Guide

| Function | Parameters | Description |
| :--- | :--- | :--- |
| `set_default_font()` | `name : str` | Sets the default font used by every `TextNode` that doesn't explicitly set its own `font` |

### Introduction

Rather than setting `font` on every single `Label`, `Button`, or other `TextNode` in your UI, you can set one default font that applies globally to any Node that doesn't override it.

```python title="Basic Usage"
cui.add_font("Poppins", "assets/fonts/Poppins-Regular.ttf")
cui.set_default_font("Poppins")

with cui.CoshUIRenderer(...):
    # Uses "Poppins" automatically since font isn't set
    cui.Label(id="my_label", text="Hello!")
```

---

### Requirements

`set_default_font()` only accepts font names that have already been registered through `add_font()`. Passing an unregistered name raises a `CoshUIError`.

```python title="Unregistered Font"
cui.set_default_font("Poppins")
# CoshUIError: That font does not exist in the system.
# Please do add_font() before this function call with the name and path as arguments.
```

---

### Overriding Per Node

Setting a default font doesn't stop individual Nodes from using their own font. Any `TextNode` with an explicit `font` value will still use that instead of the default.

```python title="Per Node Override"
cui.set_default_font("Poppins")

with cui.CoshUIRenderer(...):
    cui.Label(id="default_label", text="Uses Poppins")
    cui.Label(id="custom_label", text="Uses Courier instead", font="Courier")
```