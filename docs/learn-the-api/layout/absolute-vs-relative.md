# Positioning

### Quick Guide

| Property | Type | Default | Recursive or Local |
| :--- | :--- | :--- | :--- |
| `positioning` | CoshPositioning | CoshPositioning.RELATIVE | Local | 

### Introduction

When it comes to positioning in CoshUI, there are 2 flags that can be passed through the `positioning` attribute. 

The first is the `RELATIVE` flag. This lets the `Node` participate in layout calculations.

```python title="Setting the RELATIVE flag"
with cui.CoshUIRenderer(...):
    cui.Container(id="example_container", positioning=cui.RELATIVE)
```

This behavior sets the `Node` take in space within Containers and let other Nodes respect that space.

The second flag is the `ABSOLUTE` flag. This *lifts* the `Node` and decouples it from layout calculations aside from the parents initial `x` and `y`.

```python title="Setting the ABSOLUTE flag"
with cui.CoshUIRenderer(...):
    cui.Container(id="example_container", positioning=cui.ABSOLUTE)
```

!!! note "ABSOLUTE is Special"
    Once a `Node` is set to `ABSOLUTE`, it lets the users access the `x` and `y` attributes, which lets users manually move the Node. Do note that the position (0,0) of the `ABSOLUTE` Node is wherever its `ParentNode` starts.

??? info "CoshPositioning"
    `CoshPositioning` is the Enum that holds `RELATIVE` and `ABSOLUTE`. CoshUI has the constants `RELATIVE` and `ABSOLUTE` but it is important to know where these flags come from.

### Default Behavior

The default behavior for the `positioning` attribute is `RELATIVE`.

```python title="Default Behavior"
with cui.CoshUIRenderer(...):
    # This will be set to RELATIVE
    cui.Container(id="example_container")
```