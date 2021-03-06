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
    title: loading css
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
# how to apply CSS
<!-- #endregion -->

```javascript
// run this cell, and then 
// click the created button
tools = require('../js/tools');
tools.init();
```

<!-- #region slideshow={"slide_type": "slide"} -->
## 3 ways to apply CSS
<!-- #endregion -->

<!-- #region slideshow={"slide_type": ""} -->
* located in a separate **CSS file** - via its own URL
* embedded in html within a `<style>` html tag
* hard-attached to an element itself with `style=`
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
## preferred method : a separate CSS
<!-- #endregion -->

<!-- #region slideshow={"slide_type": ""} -->
* write your CSS in a separate file, e.g. `mystyle.css`
* which, assuming it is in the same directory as your `hello.html`
* can be kind-of included in `hello.html` 
* by inserting the following <link> line
* in the `<head>` part of your html
<!-- #endregion -->

<!-- #region cell_style="center" slideshow={"slide_type": "slide"} -->
```html
<html>
  <head>
    <!-- this is the line that matters -->
    <link rel="stylesheet" href="mystyle.css">  
  </head>
  <body>
     Hello
  </body>
</html>
```
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} tags=["level_intermediate"] -->
##### notes on relative URLs

the way we load a css from the same folder as the html, is a consequence of a general rule to build so-called *relative* URLs, that work like this:

if you have loaded a document as, say, <code>http://hostname.io/the/path/to.html</code>  
then

* <code>href="to.css"</code> is interpreted as <code>href="http://hostname.io/the/path/to.css"</code></li>
* <code>href="/to.css"</code> is interpreted as <code>href="http://hostname.io/to.css"</code></li>
* <code>href="/other/path/to.css"</code> is interpreted as <code>href="http://hostname.io/other/path/to.css"</code></li>
* <code>href="other/path/to.css"</code> is interpreted as <code>href="http://hostname.io/the/path/other/path/to.css"</code></li>

and the same goes with the <code>file:///</code> URL scheme

<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
##### notes on self-closing tags

* note also the absence of a `</link>`, 
* which may remind you of `<br>`
* such elements are called **void** or **empty** elements
* among others : `<br>`, `<hr>`, `<link>`, `<img>`,...
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
## second method : inline in html
<!-- #endregion -->

* you can also insert a `<style>` tag in your html
* and mention the CSS code there directly
* it is **less recommended** as it kind of ruins
* the desired **separation** between **contents** and **presentation**

<!-- #region slideshow={"slide_type": "slide"} -->
```html
<p> CSS can be inlined right into the HTML 
    as a <style> tag
</p>
<style>
  p {
    color: red;
    font-size: huge;
  }
</style>
```
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
## method 3: hardwired with `style=`
<!-- #endregion -->

<!-- #region slideshow={"slide_type": ""} -->
* attach a `style=` attribute on a HTML tag
* this method is by far **the worst**
* and should be used in last resort
<!-- #endregion -->

```javascript hide_input=true
embedded_html = `<p 

style="background-color: red; 
font-size: x-large; 
line-height: 50px;
padding:30px;"

>

If you attach styling to a HTML tag with a
<code>style=</code> attribute, it will 
likely take precedence on
everything else;
more on this later on

</p>`;
tools.two_columns(embedded_html)
```

<!-- #region slideshow={"slide_type": "slide"} -->
## practice
<!-- #endregion -->

<!-- #region slideshow={"slide_type": ""} hide_input=true -->
* copy `hello.html` into `mycv.html`
* create a more realistic skeleton for a résumé
  * with 4 sections 'experience', 'education', 'skills' and 'languages'
  * keep it simple for now, nothing too elaborate
  * make sure all the text gets attached to  
    adapted tags like `<p>` or `<li>` 
  * and **not** directly under `<body>`  
    like it was done in `hello.html`
  * make sure to insert at least one `<a href=...>` hyperlink
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
### practice (continued)
<!-- #endregion -->

<!-- #region slideshow={"slide_type": ""} hide_input=true -->
* create a CSS file `mycv.css`
  * with some settings that should apply to `mycv.html`
* add a `<link>` tag in the html `<head>` area
  * so the css is loaded by the html
* load `mycv.html` in a browser
  * change the CSS and reload the browser page
  * to see the effect of your changes
* we recommend you use a local git repo all along
<!-- #endregion -->

<!-- #region slideshow={"slide_type": "slide"} -->
## the browser cache
<!-- #endregion -->

for performance reasons primarily :

* fetching a file may be slow in poor network conditions
* once a file has been loaded
  * it may be **cached inside** the browser
  * so that future references do not fetch it again

**beware of that** during development

* reloading the html file
* may **not reload** the css because it is cached

<!-- #region slideshow={"slide_type": "slide"} -->
## the browser cache (continued)
<!-- #endregion -->

a couple hints and workarounds

* reload with the 'Shift' modifier pressed  
  either with a mouse-click (&#x21bb;),  
  or keyboard shortcut (⌘-r on e.g. chrome/mac)  
  double-check that with the browser you actually use
* devel tools have a *Sources* tab that let you check  
  the content of each individual loaded file
* often browsers have more advanced tools to manage cache  
  e.g. Chrome : `⠸` menu → *More Tools* → *Clear Browsing Data*
