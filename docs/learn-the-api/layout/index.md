# Overview

When making a `Node`, if you want to change certain properties that affects the engine's layouting, you need to pass in a `CoshLayout` object to the `layout` field.

```python title="Example" linenums="1" hl_lines="2"
with CoshUIRenderer(...):
    with Container(id="main_container", layout=CoshLayout()):
        pass
```

---

## CoshLayout

The `layout` field will expect a `CoshLayout` object. Now, what is CoshLayout? Well it's the object that holds all the data that is used in the engine's layout math. It looks like this:

```python title="CoshLayout" linenums="1"
@dataclass
class CoshLayout:
    true_position : tuple = (0, 0) 
    width : float | None = None
    height : float | None = None
    padding : float = 0.0
    margin : float = 0.0
```

These 5 properties make up the entirety of CoshUI's layout system. To learn more about these properties, keep reading.

---

## Width and Height

The width and height — as the name suggests — acts as the size of the object. These 2 properties are one of the most "conditional" properties in the engine.  

To learn more [click here.](width-and-height.md)

---

## Padding and Margin

The padding and margin properties work exactly as you think it does. Similar to CSS, padding will determine the taken up space for all for sides **within** nodes, and margin will determine the taken up space for all sided **outside** nodes.

To learn more [click here.](padding-and-margin.md)

---

## Position

CoshLayout has a `true_position` property which determines it's position in the layout. This usually cannot be manipulated **UNLESS** the `positioning` field of the node is set to `CoshPositioning.ABSOLUTE`.

To learn more [click here.](position.md)