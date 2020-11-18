---
title: reveal.js – The HTML Presentation Framework
date: 20.03.2016
author: Hakim El Hattab
description: A framework for easily creating beautiful presentations using HTML
separator: "^\r?\n---\r?\n$"
verticalSeparator: "^\r?\n   ---\r?\n$"
theme: black
template: ./custom/templates/default.html
css: ./custom/styles/default.css
highlightTheme: monokai
---

[![reveal.js logo](https://static.slid.es/reveal/logo-v1/reveal-white-text.svg)<!-- .element: style="height: 180px; margin: 0 auto 4rem auto; background: transparent;" class="demo-logo" -->](https://revealjs.com)

### The HTML Presentation Framework

<small>Created by [Hakim El Hattab](http://hakim.se) and [contributors](https://github.com/hakimel/reveal.js/graphs/contributors)</small>

---

## Hello There

reveal.js enables you to create beautiful interactive slide decks using HTML. This presentation will show you examples of what it can do.

---

<!-- Example of nested vertical slides -->
## Vertical Slides

Slides can be nested inside of each other.

Use the _Space_ key to navigate through all slides.

<br />

[![Down arrow]()<!-- .element: class="r-frame" style="background: rgba(255,255,255,0.1);" width="178" height="238" data-src="https://static.slid.es/reveal/arrow.png" -->](#)<!-- .element: class="navigate-down" -->

   ---

## Basement Level 1

Nested slides are useful for adding additional detail underneath a high level horizontal slide.

   ---

## Basement Level 2

That's it, time to go back up.

<br />

<a href="#/2">
	<img class="r-frame" style="background: rgba(255,255,255,0.1); transform: rotate(180deg);" width="178" height="238" data-src="https://static.slid.es/reveal/arrow.png" alt="Up arrow">
</a>

---

## Slides

Not a coder? Not a problem. There's a fully-featured visual editor for authoring these, try it out at [https://slides.com](https://slides.com).

---

<!-- .slide: data-visibility="hidden" -->
## Hidden Slides

This slide is visible in the source, but hidden when the presentation is viewed. You can show all hidden slides by setting the `showHiddenSlides` config option to `true`.

---

<!-- .slide: data-auto-animate -->
## Pretty Code<!-- .element: data-id="code-title" -->

```js []
import React, { useState } from 'react';

function Example() {
	const [count, setCount] = useState(0);

	return (
		...
	);
}
```
<!-- .element: data-id="code-animation" -->

Code syntax highlighting courtesy of [highlight.js](https://highlightjs.org/usage/).

---

<!-- .slide: data-auto-animate -->
## With animations<!-- .element: data-id="code-title" -->


```js [4,8-11|17|22-24]
import React, { useState } from 'react';

function Example() {
	const [count, setCount] = useState(0);

	return (
		<div>
			<p>You clicked {count} times</p>
			<button onClick={() => setCount(count + 1)}>
				Click me
			</button>
		</div>
	);
}

function SecondExample() {
	const [count, setCount] = useState(0);

	return (
		<div>
			<p>You clicked {count} times</p>
			<button onClick={() => setCount(count + 1)}>
				Click me
			</button>
		</div>
	);
}
```
<!-- .element: data-id="code-animation" -->

---

## Point of View

Press **ESC** to enter the slide overview.

Hold down the **alt** key (**ctrl** in Linux) and click on any element to zoom towards it using [zoom.js](http://lab.hakim.se/zoom-js). Click again to zoom back out.

(NOTE Use ctrl + click in Linux.)

---

<!-- .slide: data-auto-animate data-auto-animate-easing="cubic-bezier(0.770, 0.000, 0.175, 1.000)" -->
## Auto-Animate

Automatically animate matching elements across slides with [Auto-Animate](https://revealjs.com/auto-animate/).

<div class="r-hstack justify-center">
	<div data-id="box1" style="background: #999; width: 50px; height: 50px; margin: 10px; border-radius: 5px;"></div>
	<div data-id="box2" style="background: #999; width: 50px; height: 50px; margin: 10px; border-radius: 5px;"></div>
	<div data-id="box3" style="background: #999; width: 50px; height: 50px; margin: 10px; border-radius: 5px;"></div>
</div>

---

<!-- .slide: data-auto-animate data-auto-animate-easing="cubic-bezier(0.770, 0.000, 0.175, 1.000)" -->
<div class="r-hstack justify-center">
	<div data-id="box1" data-auto-animate-delay="0" style="background: cyan; width: 150px; height: 100px; margin: 10px;"></div>
	<div data-id="box2" data-auto-animate-delay="0.1" style="background: magenta; width: 150px; height: 100px; margin: 10px;"></div>
	<div data-id="box3" data-auto-animate-delay="0.2" style="background: yellow; width: 150px; height: 100px; margin: 10px;"></div>
</div>

## Auto-Animate<!-- .element: style="margin-top: 20px;" -->

---

<!-- .slide: data-auto-animate data-auto-animate-easing="cubic-bezier(0.770, 0.000, 0.175, 1.000)" -->
<div class="r-stack">
	<div data-id="box1" style="background: cyan; width: 300px; height: 300px; border-radius: 200px;"></div>
	<div data-id="box2" style="background: magenta; width: 200px; height: 200px; border-radius: 200px;"></div>
	<div data-id="box3" style="background: yellow; width: 100px; height: 100px; border-radius: 200px;"></div>
</div>

## Auto-Animate<!-- .element: style="margin-top: 20px;" -->

---

## Touch Optimized

Presentations look great on touch devices, like mobile phones and tablets. Simply swipe through your slides.

---

## Markdown support

Write content using inline or external Markdown.
Instructions and more info available in the [docs](https://revealjs.com/markdown/).

```md []
<section data-markdown>
  ## Markdown support

  Write content using inline or external Markdown.
  Instructions and more info available in the [docs](https://revealjs.com/markdown/).
</section>
```

---

Add the `r-fit-text` class to auto-size text

## FIT TEXT<!-- .element: class="r-fit-text" -->

---

<!-- .slide: id="fragments" -->
## Fragments

Hit the next arrow...

... to step through ...<!-- .element: class="fragment" -->

<span>... a </span><!-- .element: class="fragment" -->
<span>fragmented </span><!-- .element: class="fragment" -->
<span>slide.</span><!-- .element: class="fragment" -->

notes: This slide has fragments which are also stepped through in the notes window.

   ---

## Fragment Styles

There's different types of fragments, like:

grow<!-- .element: class="fragment grow" -->

shrink<!-- .element: class="fragment shrink" -->

fade-out<!-- .element: class="fragment fade-out" -->

<span>fade-right, </span><!-- .element: style="display: inline-block;" class="fragment fade-right" -->
<span>up, </span><!-- .element: style="display: inline-block;" class="fragment fade-up" -->
<span>down, </span><!-- .element: style="display: inline-block;" class="fragment fade-down" -->
<span>left</span><!-- .element: style="display: inline-block;" class="fragment fade-left" -->

fade-in-then-out<!-- .element: class="fragment fade-in-then-out" -->

fade-in-then-semi-out<!-- .element: class="fragment fade-in-then-semi-out" -->

Highlight
<span>red </span> <!-- .element: class="fragment highlight-red" -->
<span>blue </span> <!-- .element: class="fragment highlight-blue" -->
<span>green</span><!-- .element: class="fragment highlight-green" -->

---

<!-- .slide: id="transitions" -->
## Transition Styles

You can select from different transitions, like:<br />
[None](?transition=none#/transitions) - [Fade](?transition=fade#/transitions) - [Slide](?transition=slide#/transitions) - [Convex](?transition=convex#/transitions) - [Concave](?transition=concave#/transitions) - [Zoom](?transition=zoom#/transitions)

---

<!-- .slide: id="themes" -->
## Themes

reveal.js comes with a few themes built in:<br />
<!-- Hacks to swap themes after the page has loaded. Not flexible and only intended for the reveal.js demo deck. -->
[Black (default)](#)<!-- .element: onclick="document.getElementById('theme').setAttribute('href','css/theme/black.css'); return false;" --> -
 [White](#)<!-- .element: onclick="document.getElementById('theme').setAttribute('href','css/theme/white.css'); return false;" --> -
 [League](#)<!-- .element: onclick="document.getElementById('theme').setAttribute('href','css/theme/league.css'); return false;" --> -
 [Sky](#)<!-- .element: onclick="document.getElementById('theme').setAttribute('href','css/theme/sky.css'); return false;" --> -
 [Beige](#)<!-- .element: onclick="document.getElementById('theme').setAttribute('href','css/theme/beige.css'); return false;" --> -
 [Simple](#)<!-- .element: onclick="document.getElementById('theme').setAttribute('href','css/theme/simple.css'); return false;" --> -
 [Serif](#)<!-- .element: onclick="document.getElementById('theme').setAttribute('href','css/theme/serif.css'); return false;" --> -
 [Blood](#)<!-- .element: onclick="document.getElementById('theme').setAttribute('href','css/theme/blood.css'); return false;" --> -
 [Night](#)<!-- .element: onclick="document.getElementById('theme').setAttribute('href','css/theme/night.css'); return false;" --> -
 [Moon](#)<!-- .element: onclick="document.getElementById('theme').setAttribute('href','css/theme/moon.css'); return false;" --> -
 [Solarized](#)<!-- .element: onclick="document.getElementById('theme').setAttribute('href','css/theme/solarized.css'); return false;" -->

---

<!-- .slide: data-background="#dddddd" -->
## Slide Backgrounds

Set `data-background="#dddddd"` on a slide to change the background color. All CSS color formats are supported.

[![Down arrow]()<!-- .element: class="r-frame" style="background: rgba(255,255,255,0.1);" width="178" height="238" data-src="https://static.slid.es/reveal/arrow.png" -->](#)<!-- .element: class="navigate-down" -->

   ---

<!-- .slide: data-background="https://static.slid.es/reveal/image-placeholder.png" -->
## Image Backgrounds

```html
<section data-background="image.png">
```

```md
---

<!-- .slide: data-background="image.png" -->
```

   ---

<!-- .slide: data-background="https://static.slid.es/reveal/image-placeholder.png" data-background-repeat="repeat" data-background-size="100px"-->
## Tiled Backgrounds

```html
<section data-background="image.png" data-background-repeat="repeat" data-background-size="100px">
```

```md
---

<!-- .slide: data-background="image.png" data-background-repeat="repeat" data-background-size="100px"-->
```

   ---

<!-- .slide: data-background-video="https://s3.amazonaws.com/static.slid.es/site/homepage/v1/homepage-video-editor.mp4" data-background-color="#000000" class="black-box" -->

## Video Backgrounds

```html
<section data-background-video="video.mp4, video.webm">
```

```md
---

<!-- .slide: data-background-video="video.mp4, video.webm" -->
```

   ---

<!-- .slide: data-background="http://i.giphy.com/90F8aUepslB84.gif"-->
## ... and GIFs!

---

<!-- .slide: data-transition="slide" data-background="#4d7e65" data-background-transition="zoom" -->
## Background Transitions

Different background transitions are available via the backgroundTransition option. This one's called "zoom".

```js
Reveal.configure({ backgroundTransition: 'zoom' })
```

---

<!-- .slide: data-transition="slide" data-background="#b5533c" data-background-transition="zoom" -->
## Background Transitions

You can override background transitions per-slide.

```html
<section data-background-transition="zoom">
```

```md
---

<!-- .slide: data-background-transition="zoom" -->
```

---

<!-- .slide: data-background-iframe="https://hakim.se" data-background-interactive="" -->
<div style="position: absolute; width: 40%; right: 0; box-shadow: 0 1px 4px rgba(0,0,0,0.5), 0 5px 25px rgba(0,0,0,0.2); background-color: rgba(0, 0, 0, 0.9); color: #fff; padding: 20px; font-size: 20px; text-align: left;">

## Iframe Backgrounds

Since reveal.js runs on the web, you can easily embed other web content. Try interacting with the page in the background.

</div>

---

## Marvelous List

- No order here
- Or here
- Or here
- Or here

---

## Fantastic Ordered List

1. One is smaller than...
1. Two is smaller than...
1. Three!

---

## Tabular Tables

| Item     | Value | Quantity |
| -------- | ----- | -------- |
| Apples   | $1    | 7        |
| Lemonade | $2    | 18       |
| Bread    | $3    | 2        |

---

## Clever Quotes

These guys come in two forms, inline: <q cite="http://searchservervirtualization.techtarget.com/definition/Our-Favorite-Technology-Quotations">The nice thing about standards is that there are so many to choose from</q> and block:

> “For years there has been a theory that millions of monkeys typing at random on millions of typewriters would reproduce the entire works of Shakespeare. The Internet has proven this theory to be untrue.”

---

## Intergalactic Interconnections

You can link between slides internally, [like this](#/2/3).

---

## Speaker View

There's a [speaker view](https://revealjs.com/speaker-view/). It includes a timer, preview of the upcoming slide as well as your speaker notes.

Press the _S_ key to try it out.

notes: Oh hey, these are some notes. They'll be hidden in your presentation, but you can see them if you open the speaker notes window (hit 's' on your keyboard).

---

## Export to PDF

Presentations can be [exported to PDF](https://revealjs.com/pdf-export/), here's an example:

<iframe data-src="https://www.slideshare.net/slideshow/embed_code/42840540" marginwidth="0" marginheight="0" scrolling="no" style="border:3px solid #666; margin-bottom:5px; max-width: 100%;" allowfullscreen="" width="445" height="355" frameborder="0"></iframe>

---

## Global State

Set `data-state="something"` on a slide and `"something"` will be added as a class to the document element when the slide is open. This lets you apply broader style changes, like switching the page background.

---

<section>
<!-- .slide: data-state="customevent" -->

## State Events

Additionally custom events can be triggered on a per slide basis by binding to the `data-state` name.

```js
Reveal.on( 'customevent', function() {
	console.log( '"customevent" has fired' );
} );
```

---

<section>

## Take a Moment

Press B or . on your keyboard to pause the presentation. This is helpful when you're on stage and want to take distracting slides off the screen.

---

## Much more

- Right-to-left support
- [Extensive JavaScript API](https://revealjs.com/api/)
- [Auto-progression](https://revealjs.com/auto-slide/)
- [Parallax backgrounds](https://revealjs.com/backgrounds/#parallax-background)
- [Custom keyboard bindings](https://revealjs.com/keyboard/)

---

<!-- .slide: style="text-align: left;" -->
# THE END

- [Try the online editor](https://slides.com)
- [Source code & documentation from reveal.js](https://github.com/hakimel/reveal.js)
- [Source code & documentation from reveal-md](https://github.com/webpro/reveal-md)
