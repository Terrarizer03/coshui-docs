# Position (x and y)

### Introduction

The position for a `Node` object is rarely set as the layout engine does the work for you, but there are still certain cases where you might want to set these attributes.

```python title="Setting Position (x and y values)"
with CoshUIRenderer(...):
    with Container(id="example_container", x=10, y=10):
        pass
```

!!! info "Important"
    The `x` and `y` values from code block above will be ignored by the layout engine and will actually send a `CoshUIWarning` in the terminal as only Nodes with the `ABSOLUTE` positioning can have their `x` and `y` values set.

The main case is if your `Node` is set to `ABSOLUTE` positioning, CoshUI treats `ABSOLUTE` positioning as something *above* the `RELATIVE` Nodes. They're mostly taken out of the layout calculations aside from the initial x and y values which are inherited from the `ParentNode`.

```python title="Setting Position with ABSOLUTE"
with CoshUIRenderer(...):
    with Container(id="example_container", positioning=ABSOLUTE, x=10, y=10):
        pass
```

---

### Default Behavior

The `x` and `y` properties are special properties that rarely get manipulated. Their default values are usually always set to 0.0. The reason for this is that the layout engine determines the position for Nodes for the most part using the hidden `_x` and `_y` attributes that `x` and `y` directly manipulates when `positioning` is set to `ABSOLUTE`.