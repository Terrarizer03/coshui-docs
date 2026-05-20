# How to Install CoshUI

Thanks for wanting to try out CoshUI! Let's make this installation quick, shall we?

To install CoshUI's core, do:
```bash
pip install coshui
```

### Choose Your Backend

CoshUI is *backend-agnostic*, meaning it uses different frameworks to render its UI structure. To use those backends, you need to download their dependencies, those include:

=== "Pygame"
    ```bash
    pip install -U coshui[pygame]
    ```

=== "Raylib"
    ```bash
    pip install -U coshui[raylib]
    ```

!!! note "Upgrade"
    It's good practice to add `-U` when installing just so you update to the absolute latest. Especially in **version {{ version }}** where updates are frequent.

For more info about backends, check out the [backend section.](../learn-the-api/backends/index.md)

---

### Your First UI

Once you're done installing CoshUI and your required dependency, proceed to this [section.](your-first-ui.md)