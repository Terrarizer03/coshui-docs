---
hide:
 -navigation
---

# Changelog

This section outlines all versions and changes for CoshUI's releases and updates.

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