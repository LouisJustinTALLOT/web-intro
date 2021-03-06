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
    title: grid layout
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
# `display: grid`
<!-- #endregion -->

```javascript
// run this cell, and then 
// click the created button
tools = require('../js/tools');
tools.init();
```

<!-- #region slideshow={"slide_type": "slide"} -->
## purpose
<!-- #endregion -->

* create grid-based layouts, obviously
* historically a challenging task
  * the `<table>` tag has long been overused  
    to address that sort of needs
  * **do not use** `<table>`'s for that in 2021 !
* `grid` is now available in [all popular modern browsers](https://caniuse.com/#feat=css-grid)

<!-- #region slideshow={"slide_type": "slide"} -->
## example (1)
<!-- #endregion -->

<!-- #region cell_style="split" -->
next slide demontrates :
<!-- #endregion -->

<!-- #region cell_style="split" -->
![](../media/grid-areas.png)
<!-- #endregion -->

<!-- #region cell_style="center" -->
* a proportional grid of [3 rows ⨉ 4 columns]
* with 4 areas defined, based on that tiling
* and 4 `<div>`s that are mapped on these areas  
  *e.g.*  `grid-area: header`
<!-- #endregion -->

```javascript hide_input=true slideshow={"slide_type": "slide"}
grid1_html = `<div class="container">
<div class="item-a">the header
   <div>blabla</div></div>
<div class="item-b">main area
   <div>blabla</div><div>blabla</div></div>
<div class="item-c">side bar
   <div>blabla</div></div>
<div class="item-d">a footer
   <div>blabla</div></div>
</div>`;
grid1_css = `.container {
  display: grid;
/*  grid-template-columns: 
    1fr 1fr 1fr 1fr;*/
  grid-template-areas: 
    "header header header header"
    "main   main   .      sidebar"
    "footer footer footer sidebar";
}

.item-a {
    grid-area: header;
    background-color: #ffba5a;
}
.item-b {
    grid-area: main;
    background-color: #3282b8;
}
.item-c {
    grid-area: sidebar;
    background-color: #db3056;
}
.item-d {
    grid-area: footer;
    background-color: #7fa998;
}
`;
tools.iframe_html_css("display-grid-1", grid1_html, grid1_css, true)
```

<!-- #region cell_style="split" slideshow={"slide_type": "slide"} -->
* note the usage of a  
  *grid-specific* length unit :
<!-- #endregion -->

<!-- #region cell_style="split" -->
![](../media/grid-columns.png)
<!-- #endregion -->

<!-- #region cell_style="center" slideshow={"slide_type": ""} -->
  * `fr` stands for 'free space'
  * so we can allocate fixed or proportional space  
    to some columns (or rows, for that matter)
  * and split the rest proportionally
<!-- #endregion -->

<div class="rise-footnote">

**note** on this specific example, we could have omitted `grid-template-columns` altogether
    
</div>    

<!-- #region slideshow={"slide_type": "slide"} -->
## example (2)
<!-- #endregion -->

<!-- #region hide_input=true -->
mostly the same, but :

* we can specify fixed size for some columns
* only change is to replace
  * `grid-template-columns: 1fr 1fr 1fr 1fr` with
  * `grid-template-rows: 100px 1fr 5% 1fr;`
  
<!-- #endregion -->

<!-- #region hide_input=true -->
<div class="rise-footnote">
    
**btw** we could have written `repeat(4, 1fr)` instead of `1fr 1fr 1fr 1fr`

</div>
<!-- #endregion -->

```javascript hide_input=true slideshow={"slide_type": "slide"}
grid2_html = `<div class="container">
<div class="item-a">the header
   <div>blabla</div></div>
<div class="item-b">main area
   <div>blabla</div><div>blabla</div></div>
<div class="item-c">side bar
   <div>blabla</div></div>
<div class="item-d">a footer
   <div>blabla</div></div>
</div>`;
grid2_css = `.container {
  display: grid;
  grid-template-columns: 
    100px 1fr 5% 1fr;
  grid-template-areas: 
    "header header header header"
    "main   main   .      sidebar"
    "footer footer footer footer";
}

.item-a {
    grid-area: header;
    background-color: #ffba5a;
}
.item-b {
    grid-area: main;
    background-color: #3282b8;
}
.item-c {
    grid-area: sidebar;
    background-color: #db3056;
}
.item-d {
    grid-area: footer;
    background-color: #7fa998;
}
`;
tools.iframe_html_css("display-grid-2", grid2_html, grid2_css, true)
```

<!-- #region slideshow={"slide_type": "slide"} -->
## example (3)
<!-- #endregion -->

<!-- #region hide_input=true -->
in the previous examples :

* we have **not imposed** anything on **the height** of the result
* each box gets its height based on its content

* it is also possible - although less often needed - to fix a height globally and arrange the rows accordingly
* only change is to add on the grid:
  * `height: 100%` to say we want to use all available space
  * `grid-template-rows: 50px 1fr 100px;` which specifies how to use vertical space
`
  
<!-- #endregion -->

```javascript hide_input=true slideshow={"slide_type": "slide"}
grid3_html = `<div class="container">
<div class="item-a">the header</div>
<div class="item-b">main area</div>
<div class="item-c">side bar</div>
<div class="item-d">a footer</div>
</div>`;
grid3_css = `.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-areas: 
    "header header header header"
    "main main . sidebar"
    "footer footer footer footer";
  grid-template-rows: 50px 1fr 100px;
  height: 100%;
}

.item-a {
    grid-area: header;
    background-color: #ffba5a;
}
.item-b {
    grid-area: main;
    background-color: #3282b8;
}
.item-c {
    grid-area: sidebar;
    background-color: #db3056;
}
.item-d {
    grid-area: footer;
    background-color: #7fa998;
}
`;
tools.iframe_html_css("display-grid-3", grid3_html, grid3_css, true)
```

<!-- #region slideshow={"slide_type": "slide"} -->
## and much more…
<!-- #endregion -->

* a very good introduction to Grids  
  [can be found on css-tricks.com](https://css-tricks.com/snippets/css/complete-guide-grid/)
* with many illustrations and examples


### assignment


* **strongly recommended** 
  * to **bookmark that page**
  * and browse it (but entirely)  
    to get a grip of what's achievable


<div class="rise-footnote">

you may also [complete this game ](https://cssgridgarden.com/) at home if you feel like it
            
</div>            
            

<!-- #region slideshow={"slide_type": "slide"} tags=["level_intermediate"] -->
## auto-sizing
<!-- #endregion -->

<!-- #region cell_style="split" tags=["level_intermediate"] -->
* a nice feature of grid display
* is its ability to auto-organize the grid
* using an idiom based on
  * `repeat`
  * `auto-fit` 
  * `minmax`
<!-- #endregion -->

<!-- #region cell_style="split" tags=["level_intermediate"] -->
* that we illustrate in the next example  
* see [this doc about minmax()](https://developer.mozilla.org/en-US/docs/Web/CSS/minmax)
* see also [this blogpost on css-tricks.com](https://css-tricks.com/auto-sizing-columns-css-grid-auto-fill-vs-auto-fit/)
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} tags=["level_intermediate"] -->
## auto-sizing example
<!-- #endregion -->

```javascript hide_input=true tags=["level_intermediate"]
autosize_html = `<div class="container">
  <section> 
    <h1>Section 1</h1>
    <p> Lorem ipsum dolor sit amet, 
consectetur adipisicing elit, sed do
eiusmod tempor incididunt ut labore
et dolore magna aliqua</p> 
  </section>
  <section>
    <h1>Section 2</h1>
  </section>
  <section>
    <h1>Section 3</h1>
  </section>
</div>`;
autosize_css = `section {
  border: 1px solid blue;
  border-radius: 5px;
  margin: 2px;
}

.container {
  display: grid;
  grid-template-columns: 
    repeat(auto-fit, minmax(250px, 1fr));
}`;
tools.iframe_html_css("autosize", autosize_html, autosize_css, true)
```

<!-- #region slideshow={"slide_type": "slide"} -->
## devel tools and multi-device
<!-- #endregion -->

* the devel tools - on chrome at least 
* allow to simulate other devices
* like popular phones and tablets  

<!-- #region slideshow={"slide_type": "slide"} -->
![](../media/devel-tools-devices.png)
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
![](../media/devel-tools-phone.png)
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
## other tricks
<!-- #endregion -->

when using these technologies, you are often in a position to **add wrapping tags** in your html

to do this easily under vs-code :

* select the text you want to wrap
* enter the palette - the swiss knife in vs-code  
  (mac: ⌘-⇧-p - Windows ⌃-⇧-p - in doubt, ask google)
* type `Emmet wrap with abbreviation`
* enter the tag name



it is easy to bind a keyboard shortcut to functions that you use often


<!-- #region slideshow={"slide_type": "slide"} -->
if you need to add a wrapping `<div>` / `</div>` around some text, select it

![](../media/vs-code-0.png)
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
![](../media/vs-code-1.png)
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
then activate the palette and search for 'emmet: wrap with abbreviation'

select that funtion, you will be prompted for the name of the wrapping tag

![](../media/vs-code-2.png)
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
it is rather straightforward to attach a custim keybinding to that function if you use it often

![](../media/vs-code-3.png)
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
for example here, for now we can type 'Alt-o' to call that function

![](../media/vs-code-4.png)
<!-- #endregion -->
