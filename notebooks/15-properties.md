---
jupyter:
  celltoolbar: Slideshow
  jupytext:
    cell_metadata_filter: all,-hidden,-heading_collapsed,-run_control,-trusted
    formats: md
    notebook_metadata_filter: all,-language_info,-toc,-jupytext.text_representation.jupytext_version,-jupytext.text_representation.format_version
    text_representation:
      extension: .md
      format_name: markdown
  kernelspec:
    display_name: Javascript (Node.js)
    language: javascript
    name: javascript
  nbhosting:
    title: css properties
  rise:
    autolaunch: true
    slideNumber: c/t
    start_slideshow_at: selected
    theme: sky
    transition: cube
---

<div class="licence">
<span>Licence CC BY-NC-ND</span>
<span>Thierry Parmentelat</span>
</div>

<!-- #region slideshow={"slide_type": ""} -->
# CSS main properties
<!-- #endregion -->

```javascript
// run this cell, and then
// click the created button
tools = require('../js/tools');
tools.init();
```

<!-- #region slideshow={"slide_type": "slide"} -->
## too many to be listed

<!-- #endregion -->

* more than 100 properties defined  
  in the standard ([see full list here](https://www.w3schools.com/cssref/))
* we just mention the most obviously needed

<!-- #region slideshow={"slide_type": "slide"} -->
## text properties
<!-- #endregion -->

```javascript slideshow={"slide_type": ""} cell_style="center" hide_input=true
text_html = `<p class="text">
a sample text</p>`;
text_css = `.text {
    font-family: times;
    font-size: 30px;
    font-weight: bold;
    font-style: italic;
    text-decoration: underline;
}
`;
tools.iframe_html_css("text-properties", text_html, text_css)
```

<!-- #region slideshow={"slide_type": "slide"} -->
## many fonts available
<!-- #endregion -->

* see for example [a collection of google fonts](https://fonts.google.com/)
* note also some less traditional fonts
  * that come with usual symbols
  * see [in particular *fontawesome*](https://fontawesome.com/icons?d=gallery&m=free)  
    who offer a decent collection for free

the example below illustrates how to load and use them in your page


```javascript hide_input=true slideshow={"slide_type": "slide"}
tools.iframe_samples_html_css("font-demo")

```

<!-- #region slideshow={"slide_type": "slide"} -->
### notes on the fonts example (1)
<!-- #endregion -->

<!-- #region slideshow={"slide_type": ""} -->
* for cosmetic reasons, the example is a bit simplified  
  use something like this to import a font  
  in all variants of bold/italic

```html
<link rel="stylesheet"
      href="https://fonts.googleapis.com/css?family=Raleway:200,200i,400,400i,500,500i,600,600i,700,700i">
```
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
### notes on the fonts example (2)
<!-- #endregion -->

<!-- #region slideshow={"slide_type": ""} -->
* the single CSS rule here allows to apply  
  the font **to the whole document**  
  we will see in a moment how that actually works  

* btw, it is strongly recommended to avoid  
  mixing fonts in a document
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
### notes on the fonts example (3)
<!-- #endregion -->

<!-- #region slideshow={"slide_type": ""} -->
* also observe the import and use of *fontawesome*  
  to display custom symbols before address and phone number  

```html
<span class="fa fa-home">
```

* these symbols are more convenient than bitmap pictures  
  in particular can be safely scaled / colorized
  using CSS
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} tags=[] -->
## Unicode characters
<!-- #endregion -->

* also remember there are more than 140.000 characters defined in the Unicode standard; so without the need to switch to another font, you can just write things like these  
  ︙→ ⇀ « » ❯ × ∑ ∀α ∃ε ∈ x² © …

* being part of a text, these can also be safely styled  
  i.e. scaled, coloured&hellip;  
  as opposed to using bitmap pictures
  <span style="color:blue; background-color: gray; margin: 20px; font-size: 20px; display: flex; justify-content: center;">
    ︙→ ⇀ « » ❯ × ∑ ∀α ∃ε ∈ x² © …
</span>

<!-- #region slideshow={"slide_type": "slide"} cell_style="split" tags=[] -->
### Unicode - the easy way
<!-- #endregion -->

<!-- #region slideshow={"slide_type": ""} cell_style="split" -->
if you need to insert e.g. the ℃
symbol, you can do it several ways :

easiest way : just cut-and-paste it right into the html as-is  
(provided that your html file is utf8-encoded)
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} cell_style="split" tags=["level_intermediate"] -->
### Unicode - the less easy way
<!-- #endregion -->

<!-- #region slideshow={"slide_type": ""} cell_style="split" -->
each Unicode character has a unique codepoint

you can use that in a pure-ASCII source, and  write either

* `&#8451;` (decimal) or
* `&#x2103;`  
  the `x` stands for hexa
<!-- #endregion -->

<!-- #region cell_style="split" -->
<img src="../media/unicode-celsius.png" width="350px">
<!-- #endregion -->

<!-- #region cell_style="split" -->
<img src="../media/convert-unicode.png" width="350px">

<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} tags=["level_intermediate"] -->
### Unicode - epilogue
<!-- #endregion -->

some characters can be inserted with the same `&...;` notation using nicknames instead of a codepoint, examples

* `&lt;` for &lt; and `&gt;` for &gt;  
  sometimes useful to actually insert brackets like in &lt;code&gt;
* `&nbspc;` for a non-breaking&nbsp;space  
  which is more explicit/readable
* `&hellip;` for &hellip;


<!-- #region slideshow={"slide_type": "slide"} -->
## the box model
<!-- #endregion -->

each visible element can be styled according to the box model,  
as shown in the browser devel tools

<!-- #region cell_style="split" -->
![](../media/box-model.png)
<!-- #endregion -->

<!-- #region cell_style="split" slideshow={"slide_type": ""} -->
* padding is **inside the border**
* margin is **outside the border**

<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
## atomic properties (1)
<!-- #endregion -->

each side (top, right, bottom, left) of the box  
has its own individual properties  
here e.g. padding and border

```javascript hide_input=true
box1_html = `<p class="box1">
a box </p></div>`;
box1_css = `p.box1 {
    font-size: x-large;
    background-color: #ccc;

    padding-top: 10px;
    padding-right: 20px;
    padding-bottom: 5px;
    padding-left: 40px;

    border-bottom-width: 5px;
    border-bottom-color: black;
    border-bottom-style: solid;
}`;
tools.iframe_html_css("box1", box1_html, box1_css);
```

<!-- #region slideshow={"slide_type": "slide"} -->
### atomic properties (2)
<!-- #endregion -->

<!-- #region hide_input=true -->
again with also margin and border-radius
<!-- #endregion -->

```javascript hide_input=true
box2_html = `<p class="box2">
a second box </p>`;
box2_css = `p.box2 {
    font-size: x-large;

    background-color: #ccc;

    padding-left: 40px;
    padding-top: 10px;

    margin-left: 20px;
    margin-top: 30px;

    border-top-width: 5px;
    border-top-color: black;
    border-top-style: solid;

    border-left-width: 10px;
    border-left-color: red;
    border-left-style: solid;

    border-top-left-radius: 5px;
}`;
tools.iframe_html_css("box2", box2_html, box2_css);
```

<!-- #region slideshow={"slide_type": "slide"} -->
## shorthand properties
<!-- #endregion -->

of course this can become quite tedious,  
so there also are so-called *shorthand properties*  
for dealing with paddings, margins, borders and fonts, among others  
that allow to set **several** atomic properties in one line

<!-- #region slideshow={"slide_type": "slide"} -->
### shorthand order
<!-- #endregion -->

<!-- #region slideshow={"slide_type": ""} cell_style="split" -->
the trick is to remember this figure
<!-- #endregion -->

<!-- #region slideshow={"slide_type": ""} cell_style="split" -->
![](../media/box-sides-order.png)
<!-- #endregion -->

* `padding: 10px 20px 30px 40px` will assign the 4 padding properties in the order above
* `padding: 10px;` will set all 4 *padding* properties
* `margin: 10px 20px` will set top *and bottom* to `10px`, and *both* sides to `20px`

<!-- #region slideshow={"slide_type": "slide"} -->
### more shorthands

same kind of shorthands are available for

* `font: xxx` [see details here](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties#font_properties)
* `border: xxx` [see details here](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties#background_properties)
* for a more complete list, [see this page on MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties)
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
### shorthand example
<!-- #endregion -->

use the inspector from the devel tools to check the individual properties of the `<p>` elt, e.g. the `padding`

```javascript hide_input=true
shorthand_html = `<p class="shorthand1">
shorthand properties</p>
<hr>`;
shorthand_css = `p.shorthand1 {
    font: italic bold 20pt Arial, sans-serif;
    margin: 40px;
    padding: 30px 90px;
    border: 2px solid green;
    border-radius: 10px;
}`;
tools.iframe_html_css("shorthand", shorthand_html, shorthand_css);
```

<!-- #region slideshow={"slide_type": "slide"} -->
## unit lengths
<!-- #endregion -->

a great many deal of units are available to express lengths  
[see more details on this page](https://css-tricks.com/the-lengths-of-css/) , e.g. :

* `10px`
* `1in`, `2.54cm`, `25mm`
* `20pt` (1pt = 1/72 inch)
* `2em`, `1ex`, `20ch`, relative to current font size
* `80%` typically for width and height, relative to parent element

<!-- #region slideshow={"slide_type": "slide"} -->
## colors
<!-- #endregion -->

several formats are supported to describe a color :

* common colors by name, like `red` ([see full list](https://www.w3schools.com/colors/colors_names.asp))
* RGB components like `#8000ff` that means
  * red = 0x80 = 128, green = 0x00 = 0, blue = 0xff = 255
  * all three of course are in the [0-255] range
* same in decimal:
  * `rgb(128, 0, 255)`
* opacity (in the [0-1.] range can be given as a fourth argument
  * `rgb(128, 0, 255, 0.2)` will be only 20% opaque, i.e. almost transparent

<!-- #region slideshow={"slide_type": "slide"} -->
### colors: online resources

* like always, many online sites can help pick a decent color palette
* personnally I like this one  
  https://colorhunt.co/palette
<!-- #endregion -->

<!-- #region slideshow={"slide_type": ""} -->
<p class="rise-footnote">
    note that on colorhunt you can copy a color code by just clicking it
</p>
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
## `box-sizing`
<!-- #endregion -->

the `box-sizing` property affects the way `width` and `height` properties are computed:

* `box-sizing: content-box` : only take content into account
* `box-sizing: padding-box` : account for content + padding
* `box-sizing: border-box` : content + padding + border

margins are **always excluded**

<!-- #region slideshow={"slide_type": "slide"} -->
## `box-sizing` (continued)
<!-- #endregion -->

not often needed, but typical use case is

* you want a given component to take 500px **in total**
* so the borders and paddings *push content inside*
* then use `box-sizing: border-box`

see also https://css-tricks.com/box-sizing/
that has a live demo

<!-- #region slideshow={"slide_type": "slide"} -->
## `background`
<!-- #endregion -->

there are 8 elementary properties that make an element's background

* `background-image`
* `background-position`
* `background-size`
* `background-repeat`
* `background-attachment`
* `background-origin`
* `background-clip`
* `background-color`

<!-- #region slideshow={"slide_type": "slide"} -->
## `background` (continued)
<!-- #endregion -->

most often this is set through a unique shorthand property `background`

https://css-tricks.com/almanac/properties/b/background/


also note that background

* does cover the **padding area**
* but **not** the margin area
* that is thus essentially transparent
* and styled by parent

<!-- #region slideshow={"slide_type": "slide"} -->
## `background` (demo)
<!-- #endregion -->

```javascript hide_input=true
background_html = `<div>
  <section>
      <h1> a title </h1>
      <p> paragraph </p>
   </section>
</div>
`;
background_css = `* {
    border: 1px solid black;
}
div {
    background: red;
    margin: 100px;
}
section {
    margin: 20px;
    padding: 30px;
    background: orange;
}
h1, p {
    padding: 8px;
    /* or simply */
    background-color: yellow;
}
`;
tools.iframe_html_css("background", background_html, background_css)
```

<!-- #region hide_input=true -->
<p class="rise-footnote">
    observe how the margin space has its space filled by the parent  
    use the inspector to see how the space between  
the two inner borders (h1 and p) is actully the *max* of their margins.
</p>
<!-- #endregion -->
