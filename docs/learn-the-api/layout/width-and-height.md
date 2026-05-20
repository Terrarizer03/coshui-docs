# Width and Height

### Introduction

The `width` and `height` properties can be considered some of the most important properties within CoshUI without exaggeration. They determine the space a `Node` occupies in the layout engine. Setting them is very easy:

```python title="Setting width and height"
with CoshUIRenderer(...):
    with Container(id="example_container", width=100, height=100):
        pass
```

The code-block above shows us how to set a *fixed* width and height. But there are different behaviors you can set width and height to. Like in CSS, you can set these properties to `AUTO` and `FILL`. 

The behavior for `AUTO` means it will adapt to the size of its children, mimicking CSS's `auto` behavior.

```python title="Setting width and height as AUTO"
with CoshUIRenderer(...):
    with Container(id="example_container", width=AUTO, height=AUTO):
        pass
```

!!! question "No children AUTO?"
    If you've set the width and/or height of your Container — a `ParentNode` — as `AUTO` without it having any children, the engine will fallback to `FILL`.

`FILL`'s behavior on the other hand is the opposite, it will expand its width and/or height to the size of the parent, mimicking CSS's `100%` behavior.

```python title="Setting width and height as FILL"
with CoshUIRenderer(...):
    with Container(id="example_container", width=FILL, height=FILL):
        pass
```

Of course you can also mix behavior.

```python title="Setting width and height as AUTO and FILL"
with CoshUIRenderer(...):
    with Container(id="example_container", width=AUTO, height=FILL): # And vice-versa
        pass
```

!!! info "CoshSizing"
    `CoshSizing` is the Enum that houses AUTO and FILL (e.g., `CoshSizing.AUTO` and `CoshSizing.FILL`). Though CoshUI has the `AUTO` and `FILL` constants that you can pass without needing to call the Enum, it's good to understand where these constants come from.

--- 

### Default Behavior

The default behavior for `width` and `height` is `AUTO`. For ParentNodes, if they have no children, their sizing will change from `AUTO` to `FILL`. For Widgets on the other hand, they will be set to 0 if they have no values in the *Current Theme*.

```python title="No width or height"
with CoshUIRenderer(...):
    # The default behavior of this will be AUTO
    with Container(id="example_container"):
        pass
```

!!! failure "AUTO vs FILL"
    If you put an inner `ParentNode` that has children and width and/or height that's set to `FILL` inside an outer `ParentNode` with a width and/or height that's set to `AUTO`. The inner `ParentNode` will collapse to 0.0.

    ```python title="Failure Example"
    with Container(id="main_container", direction=COLUMN, gap=15, width=AUTO, height=AUTO):
        with Container(id="sub_container", width=FILL, height=FILL, style=CoshStyling(background_color=(255, 100, 100))): # Background color to see it's sizes.
            Button(id="sub_button", text="Example", width=100, height=100)
        Button(id="settings_button", text="Settings")
        Button(id="quit_button", text="Quit")
    ```