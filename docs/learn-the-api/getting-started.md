# Getting Started

Welcome to the **Learn The API** section of CoshUI's documentation. Now it might be a little overwhelming going through the navigation bar and seeing so many pages — but worry not as this page will serve as a guide for your journey.

If you haven't already done the first tutorial for CoshUI, it is advisable to check [it out.](../introduction/your-first-ui.md) If you already have or just think you're too cool for it, then let's get on with learning the API.

---

## Layout

The Layout section will teach you all about the `CoshLayout` object, its attributes, and how it affects CoshUI's layout system.

[Start Here](layout/index.md)

---

## Styling

This section teaches you about the `CoshStyling` object, its attributes, and how each affects the appearance of Nodes.

[Start Here](styling/index.md)

---

## Themes

Themes are the base appearance of the UI. This section will talk about the different default themes, how to set them, and how to create your own theme using the `create_theme()` public function.

[Start Here](themes/index.md)

---

## Nodes

Nodes are the heart of the UI system. This section will talk about the different kinds of nodes, their default behaviours, how the engine views them, and how to set them up properly and effectively. 

[Start Here](nodes/index.md)

---

## Animation System

CoshUI comes with it's own built-in and simple animation system. This section will teach you how to set animations and use it properly within your project.

[Start Here](animations/index.md)

---

## Signals and Data Binding

This section explains the different signals a `Node` object can emit, how to capture those signals, and how to get/bind data from specific widgets to outside variables.

[Start Here](interactions/index.md)

---

## Text System

CoshUI uses the utilized backend's built-in text system to display text. This section will teach you all about how text can be used and manipulated.

[Start Here](text/index.md)

---

## Specific Properties & Functions

If you've gone through it all or are just trying to find something specific about the API, then it's best to check these sections:

[All Node Properties](properties/index.md)  
[All Public Functions](utility/index.md)

---

## Definition of Terms

**1. Universal Attribute/Property**  

- An attribute that every Node possesses.

**2. Local Attribute/Property**  

- An attribute only certain Nodes poessesses.

**3. Recursive Values**  

- Attributes that are inherited by the Node's children (e.g., `z_index`).

**4. Local Values**  

- Attributes that only affects the specified Node (e.g., `alpha`).

**5. Atomic Nodes**

- Nodes that are only made up of a single Node (e.g., `Button`).

**6. Composite Nodes**  

- Nodes that are made up of multiple Nodes (e.g., `Slider`, `Modal`, `Dropdown`)