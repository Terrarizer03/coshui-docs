# Fonts

### Registering a Font — `add_font()`

CoshUI ships with `"Courier"`, `"Inter"`, and `"Ubuntu"` built in. To use your own font, register it first with `add_font()`, giving it a name and a file path.

```python title="add_font()"
cui.add_font("Poppins", "assets/fonts/Poppins-Regular.ttf")

cui.Label(id="my_label", text="Custom font!", font="Poppins")
```

`add_font()` also accepts optional `bold`, `italic`, and `bold_italic` variant paths:

```python title="add_font() with variants"
cui.add_font(
    "Poppins",
    "assets/fonts/Poppins-Regular.ttf",
    bold="assets/fonts/Poppins-Bold.ttf",
    italic="assets/fonts/Poppins-Italic.ttf",
    bold_italic="assets/fonts/Poppins-BoldItalic.ttf"
)
```

If a variant isn't registered and gets requested (e.g. `bold=True` on a `Label` with no bold variant), CoshUI falls back to the base font and emits a warning rather than failing.

`add_font()` raises a `CoshUIError` if any given path doesn't point to a valid file. Once registered, the name can be reused across any `TextNode` in your UI, and referenced inside CoshML tags too — see [CoshML](coshml.md).

---

### Setting the Default Font — `set_default_font()`

Any `TextNode` with `font` left as `None` falls back to the *active default font* — `"Inter"` out of the box. Use `set_default_font()` to change it globally:

```python title="set_default_font()"
cui.add_font("Poppins", "assets/fonts/Poppins-Regular.ttf")
cui.set_default_font("Poppins")

cui.Label(id="my_label", text="Now defaults to Poppins")
```

`set_default_font()` raises a `CoshUIError` if the given name hasn't been registered with `add_font()` first.