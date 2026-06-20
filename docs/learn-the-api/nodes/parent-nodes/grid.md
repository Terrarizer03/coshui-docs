# Grid

### Quick Guide

| Property | Type | Default |
| :--- | :--- | :--- |
| `column_count` | `int` | `1` |
| `align` | `CoshAlign` | `START` |
| `justify` | `CoshJustify` | `START` |
| `padding` | `float` | `0.0` |
| `gap` | `float` | `0.0` |
| `width` | `float | CoshSizing | CoshPercentage` | `AUTO` |
| `height` | `float | CoshSizing | CoshPercentage` | `AUTO` |

### Introduction

`Grid` is a `ParentNode` designed for laying out children in a structured multi-column format. It arranges children into a fixed number of columns set by `column_count`, automatically wrapping into new rows as needed. It's best suited for uniform, repeating layouts like image galleries, icon grids, or dashboards.

```python title="Grid Example"
with cui.Grid(id="gallery", column_count=3, width=600, height=400, gap=8):
    for i in range(9):
        cui.Image(id=f"img_{i}", src=f"assets/{i}.png")
```

---

### Column Count

`column_count` determines how many children appear per row before wrapping. Row count is determined automatically based on the total number of children.

```python title="Column Count"
# 3 children, column_count=2 → 2 in the first row, 1 in the second
with cui.Grid(id="example", column_count=2, ...):
    cui.Button(id="btn_a", ...)
    cui.Button(id="btn_b", ...)
    cui.Button(id="btn_c", ...)
```

---

### Cell Sizing

Each cell slot is sized uniformly by dividing the available space across columns and rows. Children with a fixed size that exceeds the uniform cell size will expand their track to accommodate them. Children set to `FILL` expand to fill their cell slot.

---

### Align and Justify

`align` and `justify` control the position of the entire grid content block within the `Grid` node, not individual children within their cells.

| Property | Controls |
| :--- | :--- |
| `align` | Vertical position of the grid content block |
| `justify` | Horizontal position of the grid content block |

---

### Default Behavior

```python title="Default Behavior"
with cui.Grid(id="example"):
    # column_count=1, align=START, justify=START
    # padding=0, gap=0
    # width and height size to fit children
    ...
```