# Overview

Welcome to the backends section, as stated multiple times in this docs page, CoshUI is *backend-aagnostic* which lets users render the same UI code in different game frameworks. In the current **version {{ version }}**, there are *2 backends* for us to use. `PygameBackend` and `RaylibBackend`.

## Pygame

For the `PygameBackend`, it takes in a `pygame.Surface` object as the parameter as pygame draws using surfaces. To invoke a `PygameBackend`, set this in your `CoshUIRenderer`:

```python
# screen is the pygame.Surface
with CoshUIRenderer(PygameBackend(screen)):
    pass
```

To learn more about how `Nodes` are rendered in pygame or just want to learn deeply about how CoshUI wraps its draw calls, [click here.](pygame.md)

## Raylib

For the `RaylibBackend` — unlike pygame — it draws on the active display, thus not needing to input a parameter. Which in more ways than one is much more helpful for migration. To invoke a `RaylibBackend`, set this in your `CoshUIRenderer`:

```python
with CoshUIRenderer(RaylibBackend()):
    pass
```

To learn more about how `Nodes` are rendered in raylibpy or just want to learn deeply about how CoshUI wraps its draw calls, [click here.](raylib.md)
