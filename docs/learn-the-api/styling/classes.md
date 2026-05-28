# Classes

### Quick Guide

| Property | Type | Default | Recursive or Local |
| :--- | :--- | :--- | :--- |
| `classes` | str or list[str] | "" (empty string) | Local |

### Introduction

CoshUI features a **class system** that lets you *reuse* `CoshStyling` objects over many `Nodes`. Basically, make a Style for specific `Nodes`, and reuse that style without needing to copy and paste the `style` field over and over again.

Now, the `classes` property is not a parameter of the `style` attribute, and it also requires a few steps first before you can start adding classes to `Nodes`. To start, you need to **create** the class by calling the `add_class` function **before** your loop, giving your class a name, and passing in the `CoshStyling` object for that class with its preferred styles. 

```python title="Creating a class"
# MAKE SURE THIS IS *BEFORE* YOUR MAIN LOOP
cui.add_class("example_class", cui.CoshStyling())
```

In the code-block above, we create the class with the name "example_class", you can now pass on the styling values that you want in the `CoshStyling` object.

Once your class is ready and the `CoshStyling` has values, you can then pass on that class to your `Node` by doing this:

```python title="Passing a class"
cui.Container(id="example_container", classes="example_class")
```

This `Container` node will now use the styling set in classes, a cool thing about this is you can pass in **multiple** classes. You can use a *spaced-string* approach or a list of class names.

```python title="Passing multiple classes"
# BEFORE Loop
cui.add_class("example_class", cui.CoshStyling())
cui.add_class("example_class_2", cui.CoshStyling())
cui.add_class("example_class_3", cui.CoshStyling())

# INSIDE loop
cui.Container(id="example_container", classes="example_class example_class_2 example_class_3")
# OR
cui.Container(id="example_container", classes=["example_class", "example_class_2", "example_class_3"])
```

!!! info "Multiple Class Priority"
    When given multiple classes like this with some classes overriding style values, the class that gets added the latest (in this case "example_class_3") will win. 
    
    If "example_class" has a `background_color` set to (255, 255, 255) and "example_class_3" has its `background_color` set to (100, 100, 255), "example_class_3" will win.

Now question, if the `style` field **and** the `classes` field were filled out, what gets applied? Well, the CoshUI engine will prioritize user explicit styles, so even if this were the case:

```python title="Class vs Style"
cui.Container(id="example_container", classes="example_class", style=cui.CoshStyling())
```

Styles set values will take precedence over any values set by classes.

### Default Behavior

The default behavior of the `classes` property is an empty string ("").

```python title="Default Behavior"
with cui.CoshUIRenderer(...):
    # The classes property is set to ""
    cui.Container(id="example_container")
```