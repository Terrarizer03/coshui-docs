# Data Binding

### Quick Guide

| Widget | Bindable Value |
| :--- | :--- |
| `Slider` | Current slider value as `float` |
| `Checkbox` | Checked state as `bool` |
| `Dropdown` | Currently selected item |

### Introduction

Some Nodes in CoshUI hold an internal value that changes based on user interaction — the position of a `Slider` thumb, whether a `Checkbox` is checked, or the selected item in a `Dropdown`. Data binding lets you keep an external variable in sync with that internal value automatically using a `Ref`.

### Ref

A `Ref` is a simple wrapper around a value. You create one with an initial value, pass it to a Node's `bind` property, and CoshUI will update it whenever the Node's internal value changes.

```python title="Creating a Ref"
volume = cui.Ref(50.0)
```

You read the current value through the `.value` property:

```python title="Reading a Ref"
print(volume.value)
```

### Usage

Pass the `Ref` to a bindable Node's `bind` property:

```python title="Binding a Slider"
volume = cui.Ref(50.0)

with cui.CoshUIRenderer(...):
    cui.Slider(id="volume_slider", min_value=0, max_value=100, bind=volume)
    cui.Label(id="volume_label", text=f"Volume: {volume.value}")
```

The `Ref` is updated automatically as the user drags the slider, so `volume.value` always reflects the current slider position.

### Supported Nodes

#### Slider
Binds the current slider value as a `float`, updated continuously as the thumb is dragged.

```python title="Slider Binding"
brightness = cui.Ref(75.0)
cui.Slider(id="brightness_slider", min_value=0, max_value=100, bind=brightness)
```

#### Checkbox
Binds the checked state as a `bool`, updated whenever the checkbox is toggled.

```python title="Checkbox Binding"
enabled = cui.Ref(False)
cui.Checkbox(id="enable_toggle", bind=enabled)
```

#### Dropdown
Binds the currently selected item from the `item_list`, updated whenever the user selects a new option.

```python title="Dropdown Binding"
selected_quality = cui.Ref("Medium")
cui.Dropdown(id="quality_dropdown", item_list=["Low", "Medium", "High"], bind=selected_quality)
```