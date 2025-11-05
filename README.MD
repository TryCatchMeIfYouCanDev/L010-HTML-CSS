# LESSON TEN - CSS Positioning and Multi-Level Navigation Menu #

## Introduction ##
This document summarises key concepts in CSS positioning, multi-level navigation menus, and best practices for creating responsive and maintainable layouts. It combines notes, practical examples, and reference links into a concise and didactic guide.

---

## 1. CSS Positioning ##
The `position` property in CSS defines how an element is placed in the document flow. By default, elements are `static` and follow the natural flow of the HTML.

| Position   | Description                                                                                                                                       |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| `static`   | Default value. Elements follow the normal document flow. Top, right, bottom, left, and z-index have no effect.                                    |
| `relative` | Element is positioned relative to its normal position. Can use top, left, bottom, right to offset. Useful as a reference for `absolute` children. |
| `absolute` | Element is positioned relative to the nearest ancestor with `position: relative`. Removed from normal flow.                                       |
| `fixed`    | Element is fixed relative to the viewport. Remains in place on scroll.                                                                            |
| `sticky`   | Element toggles between relative and fixed depending on scroll position. May not be fully supported in all browsers.                              |

### Example: Relative + Absolute ###
```html
<aside class="relative-parent">
  <div class="absolute-child">Floating Box</div>
</aside>
```
```css
.relative-parent {
  position: relative;
  width: 300px;
  height: 150px;
  border: 1px solid #000;
  overflow: hidden;
}
.absolute-child {
  position: absolute;
  width: 60px;
  height: 60px;
  bottom: 10px;
  right: 20px;
  background-color: yellow;
}
```
**Explanation:** The `.absolute-child` is positioned relative to `.relative-parent`. Changing the parent's position affects the child's reference frame.

### Controlling Overlap: `z-index` ###
Only works for elements with `position` other than `static`. Higher numbers appear above lower numbers.
```css
.element1 { position: absolute; z-index: 1; }
.element2 { position: absolute; z-index: 2; } /* appears on top */
```

### Animations with Position ###
You can animate absolute-positioned elements using `transition`:
```css
.box {
  position: absolute;
  bottom: -100px;
  transition: bottom 1s;
}
.parent:hover .box {
  bottom: 0;
}
```
This allows smooth movement of elements on hover.

---

## 2. Multi-Level Navigation Menu ##
To create a responsive dropdown menu, the key is **positioning** and **hover interactions**. Always set `<li>` as `position: relative` and `<ul>` of child menus as `position: absolute`.

### HTML Structure Example ##
```html
<nav>
  <ul>
    <li><a href="#">Home</a></li>
    <li>
      <a href="#">Courses</a>
      <ul>
        <li><a href="#">Front End</a></li>
        <li>
          <a href="#">Back End</a>
          <ul>
            <li><a href="#">Morning</a></li>
            <li><a href="#">Evening</a></li>
          </ul>
        </li>
      </ul>
    </li>
  </ul>
</nav>
```

### CSS Snippet ###
```css
nav ul {
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  margin: 0;
  padding: 0;
}
nav ul li {
  position: relative;
  background-color: orange;
  text-align: center;
}
nav ul li ul {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
  width: 150px;
  background-color: #d2691e;
}
nav ul li:hover > ul {
  display: block;
}
```
**Key Points:**
- Top-level `<li>` are `relative`. Child `<ul>` are `absolute`.
- Nested menus can be positioned using `top` and `left` for alignment.
- Use `hover` to reveal menus. For multi-level, adjust left/right for third level.

---

## 3. CSS Reset ###
Browsers apply default styles which can vary. A CSS Reset ensures consistency across browsers.
- Popular resets: **Eric Meyer**, **Josh Comeau**.
- Reset typically removes margin, padding, and default font styles.

### Example ###
```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
```

---

## 4. Best Practices & Tips ##
- Keep menu widths flexible (`calc` or `%`) for responsive design.
- Use `flex-wrap: wrap` for top-level `<ul>` to allow wrapping on smaller screens.
- Apply colours to different levels to visually distinguish them.
- Test hover and focus states for accessibility.

---

**Useful Links**
- https://meyerweb.com/eric/tools/css/reset/
- https://clarle.github.io/yui3/yui/docs/cssreset/
- http://yui.yahooapis.com/3.18.1/build/cssreset-context/cssreset-context-min.css
- https://en.wikipedia.org/wiki/Responsive_web_design
- https://alistapart.com/article/responsive-web-design/
- https://www.joshwcomeau.com/css/custom-css-reset/#our-finished-product-11
- https://www.w3schools.com/colors/colors_names.asp
- https://htmlcolorcodes.com/color-chart/web-safe-color-chart/
- https://www.cssfontstack.com/
- https://www.fontsquirrel.com/tools/webfont-generator
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/Pseudo-classes
- https://specificity.keegan.st/#google_vignette
- https://www.w3schools.com/howto/howto_css_clearfix.asp
- https://www.freecodecamp.org/italian/news/4-ragioni-z-index/
- https://codyhouse.co/gem/mega-dropdown