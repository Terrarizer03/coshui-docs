# Mouse Filter

### Quick Guide

| Value | Behavior |
| :--- | :--- |
| `STOP` | Node receives events and blocks them from Nodes behind it |
| `PASS` | Node receives events but lets them through to Nodes behind it |
| `IGNORE` | Node receives no events |

### Introduction

By default, every Node in CoshUI consumes interaction events — if two Nodes overlap, only the one on top receives signals. The `mouse_filter` property gives you control over this behavior.

```python title="Basic Usage"
with cui.Container(id="card", ...):
    cui.Label(id="card_label", text="Hello", mouse_filter=cui.PASS)
```

`mouse_filter` is a universal property, meaning every Node has it regardless of type.

### STOP
The default behavior. The Node receives interaction events and prevents any Nodes behind it from receiving them.

```python title="STOP"
cui.Button(id="btn", mouse_filter=cui.STOP, ...)
# Nodes behind this button will not receive events while the mouse is over it
```

### PASS
The Node receives interaction events and emits signals normally, but does not block Nodes behind it from also receiving events. This is useful for decorative Nodes layered on top of interactive ones.

```python title="PASS"
with cui.Container(id="card", ...):
    # The label sits on top visually but won't block clicks on the card
    cui.Label(id="card_label", text="Hello", mouse_filter=cui.PASS)
```

### IGNORE
The Node is completely invisible to the interaction system. It emits no signals and does not block anything behind it.

```python title="IGNORE"
# This container will never receive any interaction events
cui.Container(id="bg_decoration", mouse_filter=cui.IGNORE, ...)
```

### Default Behavior

The default `mouse_filter` for all Nodes is `STOP`.