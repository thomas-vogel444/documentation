# CSS Positioning

position directives:
- top
- bottom
- left
- right

## Fixed 

Position relative to the browser window.

All other elements ignore it with respect to their own positioning.

```css
div {
    position: fixed;
    top (|| bottom): 100px;
    right (|| left): 50p;
}
```

## Absolute

Position relative to the page unless the containing element's position is also set to absolute|relative.

All other elements ignore it with respect to their own positioning.

Child element absolute position is calculated with respect to the position to its containing element.

## Relative positioning

Position relative to its original position in the container. 

All other elements still respond to the initial positioning.

## Static positioning

Default behaviour of element. It won't respond to any changes to the positioning.

## Inherit positioning

Inherits the position set in the containing element.

## Z-index

Defines the stacking order of the elements.

Elements are stacked in the ascending order of their z-indexes.

The higher the z-index, the more to the forefront it will be.

## Floating Elements

```css
div {
    float: inherit | left | right;
}
```

Other elements flow around the element

clear property: element ignores floating elements, adding a new line.

```css
h1 {
    clear: both || left || right || inherit;
}
```

## Methods for centering elements

- using margin for centering horizontally
```css
div {
    margin: 0 auto;
}
```

- using absolute positioning for centering vertically
```css
div {
    position: relative;
    top: 50%;
    margin-top: -(1/2 hight of the element)
}
```

- for centering horizontally and vertically, use a container for vertical centering and auto margin to the element.