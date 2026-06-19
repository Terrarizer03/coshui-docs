# Interactions

## Introduction
In CoshUI, capturing interaction eveents is quite easy. If you want to check whether a Node was clicked? The interaction system  helps you with that.

Since it's a pretty simple concept, let's get to how **Interactions** work in CoshUI.

---

## Signals

Signals make up the entirety of CoshUI's interaction system. Every Node emits a *signal* if that specific interaction was triggered, users can access those signals using the `get_signal()` function that CoshUI provides.

To learn more, check out the [Signals](signals.md) section.

---

## Mouse Filter

If every Node emits a signal, what if we want certain Nodes to ignore those interaction events or make it pass-through while still triggering their events and emitting their signals? The `mouse_filter` property — a [Universal Property](../getting-started.md#definition-of-terms){ data-preview } — that follows Godot, handles all of that.

To learn more, check out the [Mouse Filter](mouse-filter.md) section.

---

## Data Binding

A little off "interactions", but it's applicable for users who want internal values for certain Nodes like the value of a Slider or whether a Checkbox is checked or not. CoshUI provides that with its `Ref` system.

To learn more, check out the [Data Binding](data-binding.md) section.