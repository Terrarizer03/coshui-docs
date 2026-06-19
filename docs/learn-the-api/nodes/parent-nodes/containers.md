# Container

### Quick Guide

| Property | Type | Default |
| :--- | :--- | :--- |
| `direction` | `CoshDirection` | `ROW` |
| `align` | `CoshAlign` | `START` |
| `justify` | `CoshJustify` | `START` |
| `padding` | `float` | `0.0` |
| `gap` | `float` | `0.0` |
| `overflow` | `CoshOverflow` | `VISIBLE` |
| `width` | `float | CoshSizing | CoshPercentage` | `AUTO` |
| `height` | `float | CoshSizing | CoshPercentage` | `AUTO` |

### Introduction

`Container` is the most fundamental `ParentNode` in CoshUI. It arranges its children either horizontally or vertically depending on its `direction`, and exposes `align`, `justify`, `gap`, and `padding` to control how those children are spaced and positioned within it.

```python title="Container Example"
with cui.Container(id="root", width=400, height=200, padding=10, gap=8):
    cui.Button(id="btn_a", text="A")
    cui.Button(id="btn_b", text="B")
```

### Direction

The `direction` property controls the axis children are laid out along. `ROW` places children left to right, `COLUMN` places them top to bottom.

```python title="Direction"
with cui.Container(id="row_example", direction=cui.ROW, ...):
    cui.Button(id="btn_a", ...)
    cui.Button(id="btn_b", ...)

with cui.Container(id="col_example", direction=cui.COLUMN, ...):
    cui.Button(id="btn_a", ...)
    cui.Button(id="btn_b", ...)
```

### Align

`align` controls positioning along the **cross axis** (perpendicular to `direction`).

| Value | Behavior |
| :--- | :--- |
| `ALIGN_START` | Children are placed at the start of the cross axis |
| `ALIGN_CENTER` | Children are centered along the cross axis |
| `ALIGN_END` | Children are placed at the end of the cross axis |

### Justify

`justify` controls positioning along the **main axis** (the same axis as `direction`).

| Value | Behavior |
| :--- | :--- |
| `JUSTIFY_START` | Children are packed toward the start |
| `JUSTIFY_CENTER` | Children are centered |
| `JUSTIFY_END` | Children are packed toward the end |
| `JUSTIFY_SPACE_BETWEEN` | Equal space between children, none on the edges |
| `JUSTIFY_SPACE_AROUND` | Equal space around each child |
| `JUSTIFY_SPACE_EVENLY` | Equal space between children and edges |

### Padding and Gap

`padding` adds space between the `Container`'s edges and its children. `gap` adds space between each child.

```python title="Padding and Gap"
with cui.Container(id="spaced", padding=16, gap=8, ...):
    cui.Button(id="btn_a", ...)
    cui.Button(id="btn_b", ...)
```

### Auto Sizing

When `width` or `height` is set to `AUTO`, the `Container` sizes itself to fit its children. If the `Container` has no children and is set to `AUTO`, it falls back to `FILL` with a warning.

### Default Behavior

```python title="Default Behavior"
with cui.Container(id="example"):
    # direction=ROW, align=START, justify=START
    # padding=0, gap=0, overflow=VISIBLE
    # width and height size to fit children
    ...
```