# Positioning

### Introduction

When it comes to positioning in CoshUI, there's 2 flags that can be passed through the `positioning` attribute. 

The first is the `RELATIVE` flag. This lets the `Node` participate in layout calculations.

```python title="Setting the RELATIVE flag"
with CoshUIRenderer(...):
    with Container(id="example_container", positioning=RELATIVE):
        pass
```

This behaviour sets the `Node` take in space within Containers and let other Nodes respect that space.

The second flag is the `ABSOLUTE` flag. This *lifts* the `Node` and decouples it from layout calculations.

```python title="Setting the ABSOLUTE flag"
with CoshUIRenderer(...):
    with Container(id="example_container", positioning=ABSOLUTE):
        pass
```

!!! note "ABSOLUTE is Special"
    Once a `Node` is set to `ABSOLUTE`, it lets the users access the `x` and `y` attributes, which lets users manually move the Node. Do note that the position (0,0) of the `ABSOLUTE` Node is wherever its `ParentNode` starts.

### Default Behavior

The default behavior for the `positioning` attribute is `RELATIVE`, so setting the attribute to `RELATIVE` is kind of redundant :/.

```python title="Default Behavior"
with CoshUIRenderer(...):
    # This will be set to RELATIVE
    with Container(id="example_container"):
        pass
```