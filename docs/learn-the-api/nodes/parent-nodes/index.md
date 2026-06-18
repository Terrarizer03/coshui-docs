# Overview

## Introduction
`ParentNodes` are Nodes that let you build interesting UI structures inside CoshUI in a declarative way. They are context managers, meaning they automatically deal with adding the children nodes to their actual children list, setting those children's positions based on their parameters, and sometimes even determine how much space those children take up within them. 

When something like this:

```python title="ParentNode Example"
with cui.Container(...):
    cui.Button(...):
```
is done, CoshUI does one thing, it adds the `Container` to the global CoshUI stack, and once the `Button` is initialized, the Button adds itself to the children list of the recently added `ParentNode` in the stack. Once all children have been added, the `Container` then pops itself out of the stack, which then starts the entire cycle over for other `ParentNodes`.

So now that we know what `ParentNodes` do, let's talk about the 3 different kinds of `ParentNodes` that CoshUI has; `Container`, `Grid`, and `Modal`.

---

## Container

---

## Grid

---

## Modal