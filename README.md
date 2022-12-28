# Natours

![Demo](img/Natours Project.gif)

Link to page: https://jcuetos97.github.io/Natours/
 
## Centering an element
```
parent {
  position: relative;
}

child {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

## CSS conflict resolution
1. Importance:
   User !important > Author !important > user > author > browser default
2. Same importance, higher specificity:
Inline style > id > class, pseudo class, attr > element, pseudo elements
3. Same importance, same specificity, the latter wins.


example:
```
example: 
.button { // 0 (inline), 0 (id), 1(class), 0(element)
  color: red;
}

nav#nav div.pull-right .button { // 0, 1, 2, 2
  color: yellow;
}

a { // 0, 0, 0, 1
  color: green;
}

#nav a.button:hover { // 0, 1, 2, 1
  color: white;
}

0010
0122 <- win
0001
0121
```

## How CSS values are processed
```
html, body {
  font-size: 16px;
  width: 80vw; // based on browser’s view port width
}

header {
  font-size: 150%; // reference to parent 16 * 1.5 = 24px
        /*here is different, the padding here is 24 * 2 = 48px*/
  /*for font, the ref is parent, for length/width, the ref is the current element*/
  padding: 2em; 
  margin-bottom: 10rem; // ref to root 16 * 10 = 160px
  height: 90vh;// based on browser’s view port height
  width: 1000px;
}

.header-child {
  font-size: 3em;// ref to parent 3 * 24 = 72
  padding: 10%; // reference to parent 1000 * 10 = 100px
}
```

## Visual formatting render page

1. Box-model
Content -> padding -> border -> margin (outside boxes) 
| ————— fill-area ————|

Width = content width + left border + right border + left padding + right padding
Height = content height + top border + bottom border + top padding + bottom padding

Box-sizeing: border-box; => border and padding will be include in the total width

2. block, inline, inline-block
block:
default: display block
100% parent width
Vertically one after another
Box-model applied

Inline:
Default: inline
Occupy only its content space
No line-breaks
No height and width
Padding and margin only apply to left and right
No box-model applied

Inline-block:
Default: inline-block
Occupy only is content space
No line-breaks
Box-model applied

3. Position
### Normal float
- Default: position relative
- Default position scheme
- Not floated
- Not absolute positioned
- Element layout to their source order

### Floats
- Default position float(left, right)
- Element is removed from the normal flow
- Text and inline elements will be wrapped around the flow element
- The container will not adjust its height to the element

### Absolute
- Default: position absolute
- Element is removed from the normal flow
- No impact on surrounding elements or content
- We use top, left, right, bottom to position it to its parent relative container

4. Stacking context
Z-index, the higher the more top among others
Opacity, transform, filter can also create stacking context

## CSS architecture 
- 7-1 structure
 
 +base/
 
 +components/
 
 +layout/
 
 +pages/
 
 +themes/
 
 +abstract/
 
 +vendors/

-main.scss

## Layout type
1. Float Layout
2. Flex-box
3. Css-grid

### Text with gradient
  ```
background-image: linear-gradient(to right, $color-primary-light, $color-primary-dark);
  display: inline-block;
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
```
### Hover zoom-in effect
```
&--p3 {
      left: 20%;
      top: 10rem;
      z-index: 10;
    }

    &:hover {
      transform: scale(1.05);
      box-shadow: 0 2.5rem 4rem rgba($color-black, 0.8);
      z-index: 20;
    }
```
### Flip Card Effect
https://codepen.io/anon/pen/rpMrga?editors=1100

## Background-blending
```
background-image: linear-gradient(
  to right bottom, 
  $color-secondary-light, $color-secondary-dark),
  url("../img/nat-5.jpg");
  background-blend-mode: screen;
```

### Circle layout
```
height: 12rem;
    width: 12rem;
    float: left;
    -webkit-shape-outside: circle(50% at 50% 50%);    
shape-outside: circle(50% at 50% 50%);
    -webkit-clip-path: circle(50% at 50% 50%);
    clip-path: circle(50% at 50% 50%);
```

### Background-video
```
<!-- html -->
<div class=“parent”>
<div class="bg-video">
  <video class="bg-video__content" autoplay muted loop>
    <source src="img/video.mp4" type="video/mp4">
    <source src="img/video.webm" type="video/webm">
      Your browser is not support.
    </video>
  </div>
</div>

/* css */
.bg-video {
  // add position relative to its parent
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  z-index: -1;
  opacity: 0.15;
  overflow: hidden;

  &__content {
    width: 100%;
    height: 100%;
    object-fit: cover; // will automatically remove the offset
  }
}
```

### Sibling selector
```
.a +.b {}: direct sibling, <.a/><.b/>

.a ~.b{}: indirect sibling, <.a/><.c/><.d/>...<.b/>
```

## Responsive design
1. Mobile first: min-width
2. Desktop first: max-width

Breakpoints

```
@mixin respond($breakpoint) {
  @if $breakpoint == phone {
    @media (max-width: 37.5em) { @content; } // 600px / 16
  }

  @if $breakpoint == tab-port {
    @media (max-width: 56.25em) { @content; } // 900px / 16
  }

  @if $breakpoint == tab-land {
    @media (max-width: 75em) { @content; } // 1200px / 16
  }

  @if $breakpoint == big-desktop {
    @media (min-width: 112.5em) { @content; } // 1800px / 16
  }
}
```
### Responsive image strategies
1. Resolution switching
2. Density switching
3. Art direction

## Credits 
- Design: @jonasschmedtmann
- Notes: @Jasenpan1987 
