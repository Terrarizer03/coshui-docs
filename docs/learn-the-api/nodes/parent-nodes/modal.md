# Modal

### Quick Guide

| Property | Type | Default |
| :--- | :--- | :--- |
| `width` | `float \| CoshSizing \| CoshPercentage` | `AUTO` |
| `height` | `float \| CoshSizing \| CoshPercentage` | `AUTO` |
| `direction` | `CoshDirection` | `ROW` |
| `align` | `CoshAlign` | `START` |
| `justify` | `CoshJustify` | `START` |
| `padding` | `float` | `0.0` |
| `gap` | `float` | `0.0` |
| `header_color` | `tuple(r, g, b)` | Theme default |
| `header_border_radius` | `tuple` | Theme default |
| `content_color` | `tuple(r, g, b)` | Theme default |
| `content_border_radius` | `tuple` | Theme default |
| `positioning` | `CoshPositioning` | `ABSOLUTE` |

### Introduction

`Modal` is a composite `ParentNode` for floating, draggable overlay panels. Unlike `Container` and `Grid`, it expands at runtime into two parts: a **header** that acts as a drag handle, and a **content area** that holds its children. It requires an `id` since it uses state to track its drag position across frames.

```python title="Modal Example"
with cui.Modal(id="settings_modal", width=300, height=200):
    cui.Label(id="settings_label", text="Settings")
    cui.Button(id="close_btn", text="Close")
```

### Structure

When expanded, a `Modal` with `id="my_modal"` produces the following node structure:

```python
my_modal::root       (Container, COLUMN)
├── my_modal::header (Container, drag handle)
└── my_modal::content (Container, holds children)
```


The header height is fixed at 25px with 10px padding. All children declared inside the `Modal` are placed into the content area.

### Dragging

The header acts as a drag handle automatically. Clicking and dragging it moves the entire modal, with its position persisted in state across frames.

### Styling

`header_color`, `header_border_radius`, `content_color`, and `content_border_radius` let you style the two sections independently. The default values come from the active theme.

```python title="Custom Styling"
with cui.Modal(
    id="styled_modal",
    width=300,
    height=200,
    header_color=(40, 40, 60),
    header_border_radius=(8, 8, 0, 0),
    content_color=(60, 60, 80),
    content_border_radius=(0, 0, 8, 8)
):
    ...
```

### Positioning

`Modal` defaults to `ABSOLUTE` positioning, placing it outside the normal document flow. Its position is controlled by its drag state rather than the parent layout.

### Default Behavior

```python title="Default Behavior"
with cui.Modal(id="example"):
    # positioning=ABSOLUTE, direction=ROW
    # align=START, justify=START
    # padding=0, gap=0
    # header and content colors come from the active theme
    ...
```