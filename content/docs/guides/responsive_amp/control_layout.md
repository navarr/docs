---
$title: Layout & Media queries
$order: 1
---
[TOC]

AMP supports both **media queries** &amp; **element queries**, plus comes with a powerful, built-in way to control the **layout** of individual elements. The `layout` attribute makes working with and creating fully responsive design much easier than if you'd use CSS alone.

## Responsive images, made easy

Create responsive images by specifying the `width` and `height`, setting layout to `responsive`,
and indicating with [`srcset`](/docs/guides/responsive/art_direction.html)
which image asset to use based on varying screen sizes:

[sourcecode:html]
<amp-img
    src="/img/narrow.jpg"
    srcset="/img/wide.jpg 640w,
           /img/narrow.jpg 320w"
    width="1698"
    height="2911"
    layout="responsive"
    alt="an image">
</amp-img>
[/sourcecode]

This `amp-img` element automatically fits the width
of its container element,
and its height is automatically set to the aspect ratio
determined by the given width and height. Try it out by resizing this browser window:

<amp-img src="/static/img/background.jpg" width="1920" height="1080" layout="responsive"></amp-img>

<aside class="success">
  <strong>Tip:</strong>
  <span>See our side-by-side live demo of <code>amp-img</code> for a basic and advanced example: <a href="https://ampbyexample.com/components/amp-img/">Live Demo</a></span>
</aside>

## The layout attribute

The `layout` attribute gives you easy, per-element control over how your element
should render on screen. Many of these things are possible with pure CSS – but
they're much harder, and require a myriad of hacks. Use the `layout` attribute instead.

### Supported values for  the `layout` attribute

The following values can be used in the `layout` attribute:

<table>
  <thead>
    <tr>
      <th data-th="Layout type" class="col-twenty">Layout type</th>
      <th data-th="Width/height required" class="col-twenty">Width/height required</th>
      <th data-th="Behavior">Behavior</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Layout type" class="col-twenty"><code>nodisplay</code></td>
      <td data-th="Description" class="col-twenty">No</td>
      <td data-th="Behavior">Element not displayed. This layout can be applied to every AMP element. The component takes up zero space on the screen as if its display style was none. It’s assumed that the element can display itself on user action, for example, <a href="/docs/reference/extended/amp-lightbox.html"><code>amp-lightbox</code></a>.</td>
    </tr>
    <tr>
      <td data-th="Layout type" class="col-twenty"><code>fixed</code></td>
      <td data-th="Description" class="col-twenty">Yes</td>
      <td data-th="Behavior">Element has a fixed width and height with no responsiveness supported. The only exceptions are <a href="/docs/reference/amp-pixel.html"><code>amp-pixel</code></a> and <a href="/docs/reference/extended/amp-audio.html"><code>amp-audio</code></a> elements.</td>
    </tr>
    <tr>
      <td data-th="Layout type" class="col-twenty"><code>responsive</code></td>
      <td data-th="Description" class="col-twenty">Yes</td>
      <td data-th="Behavior">Element sized to the width of its container element and resizes its height automatically to the aspect ratio given by width and height attributes. This layout works very well for most of AMP elements, including <a href="/docs/reference/amp-img.html"><code>amp-img</code></a>, <a href="/docs/reference/amp-video.html"><code>amp-video</code></a>. Available space depends on the parent element and can also be customized using <code>max-width</code> CSS.</td>
    </tr>
    <tr>
      <td data-th="Layout type" class="col-twenty"><code>fixed-height</code></td>
      <td data-th="Description" class="col-twenty">Height only</td>
      <td data-th="Behavior">Element takes the space available to it but keeps the height unchanged. This layout works well for elements such as <a href="/docs/reference/extended/amp-carousel.html"><code>amp-carousel</code></a> that involves content positioned horizontally. The <code>width</code> attribute must not be present or must be equal to <code>auto</code>.</td>
    </tr>
    <tr>
      <td data-th="Layout type" class="col-twenty"><code>fill</code></td>
      <td data-th="Description" class="col-twenty">No</td>
      <td data-th="Behavior">Element takes the space available to it, both width and height. In other words, the layout of a fill element matches its parent.</td>
    </tr>
    <tr>
      <td data-th="Layout type" class="col-twenty"><code>container</code></td>
      <td data-th="Description" class="col-twenty">No</td>
      <td data-th="Behavior">Element lets its children define its size, much like a normal HTML <code>div</code>. The component is assumed to not have specific layout itself but only act as a container. Its children are rendered immediately.</td>
    </tr>
    <tr>
      <td data-th="Layout type" class="col-twenty"><code>flex-item</code></td>
      <td data-th="Description" class="col-twenty">No</td>
      <td data-th="Behavior">Element and other elements in its parent take the parent container's remaining space when the parent is a flexible container (i.e., <code>display:flex</code>). The element size is determined by the parent element and the number of other elements inside the parent according to the <code>display:flex</code> CSS layout.</td>
    </tr>
  </tbody>
</table>

### What if width and height are undefined?

In a few cases if `width` or `height` are not specified,
the AMP runtime can default these values as the following:

* [`amp-pixel`](/docs/reference/amp-pixel.html): Both width and height are defaulted to 0.
* [`amp-audio`](/docs/reference/extended/amp-audio.html): The default width and height are inferred from browser.

### What if the <code>layout</code> attribute isn’t specified?

If the <code>layout</code> attribute isn't specified, AMP tries to infer or guess
the appropriate value:

<table>
  <thead>
    <tr>
      <th data-th="Rule">Rule</th>
      <th data-th="Inferred layout" class="col-thirty">Inferred layout</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td data-th="Rule"><code>height</code> is present and <code>width</code> is absent or equals to <code>auto</code></td>
      <td data-th="Inferred layout"><code>fixed-height</code></td>
    </tr>
    <tr>
      <td data-th="Rule"><code>width</code> or <code>height</code> attributes are present along with the <code>sizes</code> attribute</td>
      <td data-th="Inferred layout"><code>responsive</code></td>
    </tr>
    <tr>
      <td data-th="Rule"><code>width</code> or <code>height</code> attributes are present</td>
      <td data-th="Inferred layout"><code>fixed</code></td>
    </tr>
    <tr>
      <td data-th="Rule"><code>width</code> and <code>height</code> are not present</td>
      <td data-th="Inferred layout"><code>container</code></td>
    </tr>
  </tbody>
</table>

## Using media queries

### CSS media queries

Use [`@media`](https://developer.mozilla.org/en-US/docs/Web/CSS/@media)
to control how the page layout looks and behaves, as you would do on any other website.
When the browser window changes size or orientation,
the media queries are re-evaluated and elements are hidden and shown
based on the new results.

<aside class="success">
  <strong>Tip:</strong>
  <span>Learn more about controlling layout by applying media queries in
<a href="https://developers.google.com/web/fundamentals/design-and-ui/responsive/fundamentals/use-media-queries?hl=en">Use CSS media queries for responsiveness</a>.</span>
</aside>

### Element media queries

One extra feature for responsive design available in AMP is the `media` attribute.
This attribute can be used on every AMP element;
it works similar to media queries in your global stylesheet,
but only impacts the specific element on a single page.

For example, here we have 2 images with mutually exclusive media queries.

[sourcecode:html]
<amp-img
    media="(min-width: 650px)"
    src="wide.jpg"
    width=466
    height=355
    layout="responsive">
</amp-img>
[/sourcecode]

Depending on the screen width, one or the other will be fetched and rendered.

[sourcecode:html]
<amp-img
    media="(max-width: 649px)"
    src="narrow.jpg"
    width=527
    height=193
    layout="responsive">
</amp-img>
[/sourcecode]
