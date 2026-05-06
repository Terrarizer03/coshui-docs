# alpha

The alpha value controls the transparency of the Node and is a universal property (meaning every Node has this property). This node lives within the `CoshStyling` object. It can be set with both the alpha field (e.g. `alpha=100`) and the background_color field (e.g. `background_color=(255, 0, 0, 100)`) as the 4th value. 

??? info "Important Info"
    !!! note "Property Precedence"
        If you have alpha set in **both** the `alpha` and `background_color` field, the `alpha` field will be applied as the engine treats it as higher priority.

    !!! note "Recursive or Local"
        The alpha value is local thus it does not affect the alpha values of its children. If a container had `alpha=100`, its children will not inherit that value.
    


### Type

The `alpha` value can be `int | None`.

### Default/Sentinel Value

`None`.

??? note "Default Value"
    Although the Sentinel Value is `None`, the Engine itself treats this `None` value as `255` (max opacity). So if users don't explicitly set the alpha value, it will be fully opaque.

### Min/Max Values

The minimum value of this property is `0` with the maximum being `255`.

## Examples

```python linenums="1"
with CoshUIRenderer(...):
    with Container(...):
        Button(text="Hello", style=CoshStyling(alpha=100))
```

or

```python linenums="1"
with CoshUIRenderer(...):
    with Container(...):
        Button(text="Hello", style=CoshStyling(background_color=(255, 0, 0, 100)))
```

