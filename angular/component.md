# Component

Refer angular\template_syntax.md
`https://angular.io/start`

Components define areas of responsibility in your UI that let you reuse these sets of UI functionality.

## component is comprised of three things

### A component class

which **handles data and functionality**. In the previous section, the `product data` and the `share()` method were defined for you in the component class.

### A HTML template

which determines **what is presented to the user**. In the previous section, you modified the product list's HTML template to display the name, description, and a "Share" button for each product.

### Component-specific styles

that define the look and feel. The product list does not define any styles.

An Angular application is composed of a tree of components, in which each Angular component has a specific purpose and responsibility.

### Providers

An array of providers for services that the component requires

## Example UI

![app-component](https://angular.io/generated/images/guide/start/app-components.png)

### Example explanation

- `app-root` (orange box) is the application shell. This is the first component to load, and the parent of all other components or we can call it base component
- `app-top-bar` (blue background) is the store name and checkout button.
- `app-product-list` (purple box) is the product list that you modified in the previous section.

## Component Interaction
