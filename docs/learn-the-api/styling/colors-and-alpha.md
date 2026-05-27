# Colors and Alpha

### Introduction

In UI libraries, one of the most common things people automatically reach for is *color*. Being able to change the color is normal and expected. In CoshUI, changing color requires passing in a `CoshStyling` object to a universal `style` field and adding an `RGB` or `RGBA` tuple to the `background_color` field.

```python title="Setting color"
with cui.CoshUIRenderer(...):
    with cui.Container(id="example_container", style=cui.CoshStyling(background_color=(255, 255, 100))):
```

Now we get onto why **Color** and **Alpha** was added to the same page. As I discussed, you can pass in an `RGB` *or* an `RGBA` value to `background_color`.

```python title="Setting color WITH alpha"
with cui.CoshUIRenderer(...):
    # The 4th value in the background_color tuple is Alpha
    with cui.Container(id="example_container", style=cui.CoshStyling(background_color=(255, 255, 100, 255))):
```

In the code block above, we set a 4th value in the tuple that acts as the `alpha` field. But that isn't the only way to set `alpha`.

```python title="Setting alpha"
with cui.CoshUIRenderer(...):
    with cui.Container(id="example_container", style=cui.CoshStyling(alpha=255)):
```

There is also a dedicated `alpha` field that you can pass in a value between 0-255 to.

!!! info "Precedence"
    If you add set the alpha value in `background_color` (background_color=(255, 255, 100, 100)) **AND** in `alpha` (alpha=255), the value within the `alpha` field takes precedence.

    ```python title="Setting both RGBA and alpha"
    with cui.CoshUIRenderer(...):
        # The alpha field takes higher priority in the engine, so in this case, 
        # the alpha value of the node is 255.
        with cui.Container(id="example_container", style=cui.CoshStyling(
            background_color=(255, 255, 100, 100), 
            alpha=255
        )):
    ```

---

### Default Behavior

When `background_color` is not set, the default value the engine takes is `None`, if the `background_color` is not set, the rectangle of the `Node` just doesn't get rendered at all.

```python title="Default Behavior"
with cui.CoshUIRenderer(...):
    # Since no explicit value is passed, background_color is set to None
    with cui.Container(id="example_container", style=cui.CoshStyling()):
```

For `alpha`, the default value is 255 — the max value — when no explicit value is passed. 

```python title="Default Behavior"
with cui.CoshUIRenderer(...):
    # Since no explicit value is passed, alpha is set to 255
    with cui.Container(id="example_container", style=cui.CoshStyling()):
```

??? note "Fun Fact"
    If `background_color` is set to `None`, `alpha` is set to 0, or both, CoshUI just doesn't bother to render that `Node`.