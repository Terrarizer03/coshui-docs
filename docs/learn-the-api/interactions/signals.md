# Signals

### Quick Guide

| Signal | Trigger |
| :--- | :--- |
| `CLICKED` | Mouse button pressed down on the Node |
| `RELEASED` | Mouse button released after a click on the Node |
| `PRESSED` | Mouse button held down on the Node |
| `HOVERED` | Mouse is over the Node |
| `HOVER_ENTER` | Mouse entered the Node's bounds |
| `HOVER_EXIT` | Mouse left the Node's bounds |

### Introduction

Signals are how CoshUI communicates interaction events. Every frame, CoshUI checks which Nodes were interacted with and emits the relevant signals for them. You can read those signals using the `get_signal()` function.

```python title="Basic Usage"
with cui.CoshUIRenderer(...):
    cui.Button(id="my_btn", text="Click Me")
    
if cui.get_signal("my_btn", cui.CLICKED):
    print("Button was clicked!")
```

`get_signal()` returns `True` if that signal was emitted for that Node this frame, and `False` otherwise.

---

### Signal Reference

#### CLICKED
Emitted on the frame the mouse button is pressed down on the Node. This fires once per click, not continuously.

```python title="CLICKED"
if cui.get_signal("my_btn", cui.CLICKED):
    print("Clicked!")
```

#### RELEASED
Emitted on the frame the mouse button is released, as long as the Node was the one originally clicked. This means even if the mouse has moved off the Node by the time the button is released, `RELEASED` will still fire on it.

```python title="RELEASED"
if cui.get_signal("my_btn", cui.RELEASED):
    print("Released!")
```

#### PRESSED
Emitted every frame the mouse button is held down while over the Node. Unlike `CLICKED`, this fires continuously.

```python title="PRESSED"
if cui.get_signal("my_btn", cui.PRESSED):
    print("Holding down...")
```

#### HOVERED
Emitted every frame the mouse is over the Node.

```python title="HOVERED"
if cui.get_signal("my_btn", cui.HOVERED):
    print("Mouse is over the button")
```

#### HOVER_ENTER
Emitted on the single frame the mouse enters the Node's bounds. Useful for triggering one-shot effects like animations.

```python title="HOVER_ENTER"
if cui.get_signal("my_btn", cui.HOVER_ENTER):
    print("Mouse just entered!")
```

#### HOVER_EXIT
Emitted on the single frame the mouse leaves the Node's bounds.

```python title="HOVER_EXIT"
if cui.get_signal("my_btn", cui.HOVER_EXIT):
    print("Mouse just left!")
```