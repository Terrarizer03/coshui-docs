# Width and Height

## The Two Ways To Set Width And Height

The `width` and `height` properties are quite special properties. Since they're commonly set, they have their own "flat-paramenters" in the `Node` object.  
So instead of needing to do this:

```python title="Set Properties in CoshLayout" linenums="1"
with CoshUIRenderer(...):
    with Container(id="main_container", layout=CoshLayout(width=100, height=100)):
        pass
```

you can actually set it like this:

```python title="Flat Parameters" linenums="1"
with CoshUIRenderer(...):
    with Container(id="main_container", width=100, height=100):
        pass
```

!!! info "Precedence"
    An extremely important detail about the 2 ways to set `width` and `height` is that if you set **both** of them for the same node, the **flat-parameters** will be prioritized by the engine.

---

## Default Behavior

The default behavior of these parameters is that if they aren't explicitly set, they will be treated to `FIT` their contents. Meaning they will take the max/total width and height of their children.

!!! note "Widgets"
    As widget Nodes don't have children, if you don't set their width and height specifically, the theme will override it if it exists for that widget or is just set to the default of `0.0`.

Another special way to set width and height is changing the `sizing` field in a Node to `CoshSizing.FILL` which will override the width and height parameters and set it so it takes up the remaining space within its parent container.

```python title="CoshSizing.FILL" linenums="1"
with CoshUIRenderer(...):
    with Container(id="main_container", sizing=CoshSizing.FILL):
        pass
```