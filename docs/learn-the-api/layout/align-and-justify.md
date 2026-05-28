# Align and Justify

### Quick Guide

| Property | Type | Default | Recursive or Local |
| :--- | :--- | :--- | :--- |
| `align` | CoshAlign | CoshAlign.START | Recursive | 
| `justify` | CoshJustify | CoshJustify.START | Recursive | 

### Introduction

CoshUI's implementation of `align` and `justify` is similar to CSS's implementation of `align-items` and `justify-content`.

!!! info "Important"
    The `align` and `justify` properties are only accessible through the `ParentNode` (i.e. `Container`, `Modal`, or `Grid`)

```python title="Setting align and justify"
with cui.CoshUIRenderer(...):
    cui.Container(id="example_container", align=cui.ALIGN_CENTER, justify=cui.JUSTIFY_CENTER)
```

Starting with the `align` property, there are 3 flags you can pass through that lets you manipulate the position of the `Nodes` within a `ParentNode`.

| Flag | Description |
| :--- | :--- |
| `ALIGN_START` | Pushes children to the start of the cross axis. |
| `ALIGN_CENTER` | Pushes children to the center of the cross axis. |
| `ALIGN_END` | Pushes children to the end of the cross axis. |

Although the data table above seems like it's stating the obvious, it's genuinely just that simple. Moving on to `justify`, this has a few more flags than `align`.

| Flag | Description |
| :--- | :--- |
| `JUSTIFY_START` | Pushes children to the start of the main axis. |
| `JUSTIFY_CENTER` | Pushes children to the center of the main axis. |
| `JUSTIFY_END` | Pushes children to the end of the main axis. |
| `JUSTIFY_SPACE_BETWEEN` | Divides and sets the gap between the children so that the first and last child reaches the very start and end of the main axis. |
| `JUSTIFY_SPACE_AROUND` | Divides and sets the gap between the children to have equal gap all around each child. |
| `JUSTIFY_SPACE_EVENLY` | Sets the gap between children so that they are *exactly* the same size. |

!!! note "Cross Axis vs Main Axis"
    If you haven't heard about those terms before, the cross axis means the perpendicular of the `direction` (e.g., `ROW` or `COLUMN`), the main axis follows along the `direction`.

??? info "CoshAlign and CoshJustify"
    `CoshAlign` and `CoshJustify` are where all of the values listed above live. The values above are the user-facing flags, but it's important to know where these flags come from.

### Default Behavior

The default behavior for `align` and `justify` is their "START" values.

```python title="Default Behavior"
with CoshUIRenderer(...):
    # This will be set to align=ALIGN_START and justify=JUSTIFY_START
    cui.Container(id="example_container")
```

!!! failure "Grid Testing"
    `align` and `justify` works a bit differently for `Grid` and may require some changes before it becomes properly documented.