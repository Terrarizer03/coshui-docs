# Overview

CoshUI's main philosophy is the idea that *everything* should have a certain level of flexibility and customization. Unlike other Python UI libraries that follow strict themes and let you use only pre-made layouts, CoshUI is fundamentally different. This section will teach you about the different kinds of attributes that you can change in the `CoshStyling` object, how it affects their looks, and how to make `classes` to reuse those styles.

!!! note "v{{ version }}"
    Do note that this is only version {{ version }} and these attributes can grow and change behavior in the future.

---

### Colors and Alpha

```python
# Background Color AND Alpha
with cui.Container(id="example_container", style=cui.CoshStyling(background_color=(255, 255, 100), alpha=100)):
# Background Color WITH Alpha
with cui.Container(id="example_container", style=cui.CoshStyling(background_color=(255, 255, 100, 100))):
```

The first style we'll discuss is the `background_color` and the `alpha` property. Although they seem like they have little to no correlation, they are actually quite coupled in the CoshUI engine along with the fact that they have slightly similar behavior. To learn more, [click here.](colors-and-alpha.md)

### Borders

```python
with cui.Container(id="example_container", style=cui.CoshStyling(border=((255, 255, 100), 5))):
# or
with cui.Container(id="example_container", style=cui.CoshStyling(border=(255, 255, 100, 5))):
```

The `border` property in CoshUI acts as the *outline* for the `Node`. It requires 2 values, a **color** for the border and its **weight**. To learn more [click here.](borders.md)

### Border Radius

```python
with cui.Container(id="example_container", style=cui.CoshStyling(border_radius=20)):
# or
with cui.Container(id="example_container", style=cui.CoshStyling(border_radius=(10, 20, 10, 20))):
```

The `border_radius` property lets you change the *roundness* of the corners of a `Node`. To learn more [click here.](border-radius.md)

### Transforms

```python
with cui.Container(id="example_container", style=cui.CoshStyling(transform_position=(50, 50), transform_rotation=45.0, transform_scale=2.0)):
```

This page will teach you about the different transforms you can do to a `Node` object, mainly `transform_position`, `transform_rotation`, and `transform_scale`. To learn more [click here.](transforms.md)

### Classes

```python
# Outside the loop
add_class("example_class", cui.CoshStyling(background_color=(255, 100, 100)))

# In CoshUIRenderer
with cui.Container(id="example_container", classes="example_class"):
```

The `classes` property in CoshUI is a way to reuse CoshStyling objects without needing to do `style=cui.CoshStyling()` throughout every `Node` object, it also lets you combine different `CoshStyling` objects in case you have multiple classes you want to reuse for a `Node`. To learn more, [click here.](classes.md)