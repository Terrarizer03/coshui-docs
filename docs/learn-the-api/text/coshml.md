# CoshML

### Introduction

CoshML is a small BBCode-style markup language for styling parts of a string. It's parsed by `RichLabel`, letting you mix multiple fonts, colors, weights, and other styles within a single block of text.

```python title="Basic Usage"
cui.RichLabel(id="my_label", text="Welcome [bold]back[/], friend!")
```

Tags open with `[tag]` and close with `[/]`. Tags can be nested, and inner tags inherit whatever style is currently active — only overriding what they explicitly set.

```python title="Nesting"
cui.RichLabel(id="my_label", text="[font=Courier]Hello [bold]World[/][/]")
```

Here, `World` is bold **and** stays in Courier, since `[bold]` doesn't touch the active font — it only adds bold on top of it.

---

### Keyword Tags

These are single-word tags that don't take a value:

| Tag | Effect |
| :--- | :--- |
| `[bold]` | Bold weight |
| `[italic]` | Italic style |
| `[underline]` | Underlines the text |
| `[strikethrough]` | Strikes through the text |
| `[red]` / `[green]` / `[blue]` / `[white]` | Sets text color |

```python title="Keyword tags"
cui.RichLabel(id="my_label", text="[bold][red]Warning:[/] please read carefully[/]")
```

---

### Attribute Tags

These take a value with `tag=value` syntax:

| Tag | Value | Example |
| :--- | :--- | :--- |
| `color` | `(r, g, b)` string | `[color=(255, 0, 0)]` |
| `font` | Registered font name | `[font=Courier]` |
| `font_size` | Integer | `[font_size=24]` |

```python title="Attribute tags"
cui.RichLabel(id="my_label", text="[color=(0, 200, 255)][font_size=24]Big blue text[/][/]")
```

Fonts referenced here must already be registered via `add_font()` — see [Fonts](fonts.md).

---

### Custom Text Classes — `add_class()`

For styles you reuse often, register a named `TextStyle` once with `add_class()`, then reference it by name as a tag:

```python title="add_class() with TextStyle"
cui.add_class("warning", cui.TextStyle(color=(255, 80, 80), bold=True))

cui.RichLabel(id="my_label", text="[warning]Careful, this can't be undone.[/]")
```

`TextStyle` accepts the same properties as the attribute tags above (`color`, `font`, `font_size`, `bold`, `italic`, `underline`, `strikethrough`). A class name can't collide with an existing tag name or another registered class — both raise a `CoshUIError`.

Note: `add_class()` is also used to register `CoshStyling` classes for general Node styling (background color, border, etc.) — passing a `CoshStyling` instead of a `TextStyle` registers a class usable via a Node's `classes` property instead of a CoshML tag. The two are separate registries, so a name can be reused as both a Node style class and a text style class.

---

### Error Handling

Malformed CoshML raises a `CoshMLError` rather than failing silently — unclosed tags, unknown tags/attributes (with a suggestion via typo-matching), and invalid values (e.g. a non-3-tuple `color`) are all caught at parse time.  