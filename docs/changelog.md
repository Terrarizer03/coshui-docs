---
hide:
 -navigation
---

# Changelog

This section outlines all versions and changes for CoshUI's releases and updates.

---
## [v0.3.0] Graphics Pipeline Support

`June 7, 2026`
### New Features:

- **CoshPercentage**: New sizing type that lets users set width/height as a percentage of the parent’s dimensions.
- **CoshDebug**: New debugger that opens its own tkinter window and shows a live node inspector showing the full UI tree, computed layout values, style properties, and signals fired each frame.
- **More Easing Curves**: Added new easing curves to `animate()`.  

<figure align=center markdown>

| New Curves |
| :---: |
| `"ease_in_bounce"` |
| `"ease_out_bounce"` |
| `"ease_in_elastic"` |
| `"ease_out_elastic"` |

</figure>

### Behavior Changes:

- **ABSOLUTE FILL**: Gave the ability for `ABSOLUTE` positioning Nodes to use cui.FILL for its `width` and `height` values.

### Breaking Changes:

- **On Complete**: `animate()` function no longer takes in on_complete callback, but returns a Tween that lets you call a `.finished()` method that accepts the callback. This is partly to make it more pythonic but also to clean up the API and to add new methods in the future like `.loop()`.
    - **Example**: `animate(...).finished(callback)`
- **Property Name Changes**: `animate()` function's property names changed. By doing this, it becomes easier to use the animation system by mapping the new names to the actual properties being animated.  

<figure align=center markdown>

| Old | New |
| :--- | :--- |
| `animate("scale", …)` | `animate("transform_scale", …)` |
| `animate("position", …)` | `animate("transform_position", …)` |
| `animate("rotation", …)` | `animate("transform_rotation", …)` |

</figure>

### Bug Fixes:

- **Pygame’s Missing Alpha**: Alpha value not being set when rotation was 0.0 for rectangles, this is due to being accidentally forgotten when implementing rotation.
- **Raylib Border-radius Rotation**: Raylib losing border radius when rotated is now fixed.

### Backends:

- **PyOpenGLBackend**: New backend for PyOpenGL with GLFW support.
- **ModernGLBackend**: New backend for ModernGL with GLFW and MGLW support.

!!! warning
    ModernGL-Window's support acts fairly weird with the debugger. My main theory is the debugger consumes a bit too much and hangs some parts of it. If this is true, then this may also be a program complexity problem — which if it is, there might become a need to completely rework the debugger.

### New Installs:
```bash
# For ModernGL + GLFW
pip install coshui[moderngl]

# For ModernGL + MGLW
pip install coshui[moderngl-mglw]

# For PyOpenGL + GLFW
pip install coshui[pyopengl]
```

### Planned for v0.3.1 and above:

- **Gradients**: Gradient support for all backends.
- **Drop Shadow**: Drop Shadow support for all backends.
- **Glow**: Glow support for all backends.
- **Profiler**: "Profile" tab in Debugger that gives context in frame by frame execution times of each engine pass.
- **More Alignment Options**: Self alignment in `Grid` cells. 
- **And Much More...**

---

## [v0.2.4] Initial Release 

`May 23, 2026`  
The first public release of CoshUI — a Python-first, declarative, backend-agnostic UI library.

### What's included
- Full layout engine with flexbox-inspired sizing (FILL, AUTO, padding, margin, gap)
- Container and Grid layout nodes
- Widget set: Button, Label, Checkbox, Slider, Modal, Image, Dropdown
- Pygame and Raylib backends
- Tween animation system with configurable easing
- Signal-based event system
- Theme and CSS-inspired class system
- Text wrapping and transform rotation support

### Install
```bash
# For core
pip install coshui

# For Pygame
pip install coshui[pygame]

# For Raylib
pip install coshui[raylib]
```

### Notes
This is an early release. Grid has not been thoroughly tested and may have edge cases. Issues and contributions welcome on [GitLab](https://gitlab.com/jylefv/CoshUI).