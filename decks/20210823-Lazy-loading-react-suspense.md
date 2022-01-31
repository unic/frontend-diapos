---
title: Lazy loading in react with suspense
date: 23.08.2021
author: Oriol Torrent Florensa
description: Using new React's Suspense feature for lazy loading components
separator: <!--h-->
verticalSeparator: <!--v-->
notesSeparator: <!--n-->
theme: ./custom/styles/dark-unic.css
css: ./custom/styles/general.css
template: ./custom/templates/general.html
highlightTheme: monokai
---

# Lazy loading in react with suspense

<!--n--> Lazy loading is a way to load content only when it is needed. This is achieved by splitting our app into multiple chunks. <br>
The idea here is to serve the user only with reduced amount of assets, and serve the rest as they request it.

<!--v-->

## Code splitting approaches

- Route based
<!-- .element: class="fragment" -->

- Component based
<!-- .element: class="fragment" -->

<!--n--> Route-based: If we can compile different routes in different bundles we can serve them as long as the user visits them.<br>
It also allows for a pre-loading mechanism similar to Gatsby: pre-load next pages based on what router-links are placed in the currently visited page.<br><br>
Component-based: It allows extracting heavy components so that the main bundle can stay in a reasonable size.


<!--h-->

## APIs

- Dynamic imports
<!-- .element: class="fragment r-fit-text" -->

- `React.lazy` and `Suspense`
<!-- .element: class="fragment r-fit-text" -->

<!--n--> To achieve this we can use `Dynamic imports`. According to MDN (links at the end), the support is very good, excluding only IE.<br><br>
`React.lazy` and `Suspense` are the tools from React that we can use to leverage the use of Dynamic imports in React. We must know, however, that React.lazy and Suspense are not yet available for server-side rendering.

<!--v-->

### Example<!-- .element: data-id="sticky-el-title" -->

```jsx []
import React from 'react'

const JustAComponent = () => {
	return (<p>This content is lazy-loaded</p>)
}

export default JustAComponent

```

<!--n--> This component does nothing, but you get the idea: it could very well be any heavy component.

<!--v-->

### Example<!-- .element: data-id="sticky-el-title" -->

```jsx []
const JustAComponent = lazy(() => import('./JustAComponent'))
```

<!--n--> To load it dynamically we would need this syntax above in order to have the component loaded in a separate chunk.<br>
The problem of this is that now we will have it in a separate file, bit that file will always be loaded. This is where intersection observer comes into play:

<!--v-->

<!-- .slide: data-background-iframe="https://react-intersection-observer.vercel.app/?path=/story/useinview-hook--lazy-hook-rendering" -->
<!-- .slide: data-background-opacity="0.3" -->
<!-- .slide: data-facts -->
### Awesome package! <span aria-hidden>📦</span>

Awesome docs!<span aria-hidden>📖</span>

Awesome [demo](https://react-intersection-observer.vercel.app) in
<svg width="200px" height="40px" viewBox="0 0 200 40" class="css-173of3" role="img"><title>Storybook</title><defs><path d="M1.2 36.9L0 3.9c0-1.1.8-2 1.9-2.1l28-1.8a2 2 0 0 1 2.2 1.9 2 2 0 0 1 0 .1v36a2 2 0 0 1-2 2 2 2 0 0 1-.1 0L3.2 38.8a2 2 0 0 1-2-2z" id="a"></path></defs><g fill="none" fill-rule="evenodd"><path d="M53.3 31.7c-1.7 0-3.4-.3-5-.7-1.5-.5-2.8-1.1-3.9-2l1.6-3.5c2.2 1.5 4.6 2.3 7.3 2.3 1.5 0 2.5-.2 3.3-.7.7-.5 1.1-1 1.1-1.9 0-.7-.3-1.3-1-1.7s-2-.8-3.7-1.2c-2-.4-3.6-.9-4.8-1.5-1.1-.5-2-1.2-2.6-2-.5-1-.8-2-.8-3.2 0-1.4.4-2.6 1.2-3.6.7-1.1 1.8-2 3.2-2.6 1.3-.6 2.9-.9 4.7-.9 1.6 0 3.1.3 4.6.7 1.5.5 2.7 1.1 3.5 2l-1.6 3.5c-2-1.5-4.2-2.3-6.5-2.3-1.3 0-2.3.2-3 .8-.8.5-1.2 1.1-1.2 2 0 .5.2 1 .5 1.3.2.3.7.6 1.4.9l2.9.8c2.9.6 5 1.4 6.2 2.4a5 5 0 0 1 2 4.2 6 6 0 0 1-2.5 5c-1.7 1.2-4 1.9-7 1.9zm21-3.6l1.4-.1-.2 3.5-1.9.1c-2.4 0-4.1-.5-5.2-1.5-1.1-1-1.6-2.7-1.6-4.8v-6h-3v-3.6h3V11h4.8v4.6h4v3.6h-4v6c0 1.8.9 2.8 2.6 2.8zm11.1 3.5c-1.6 0-3-.3-4.3-1a7 7 0 0 1-3-2.8c-.6-1.3-1-2.7-1-4.4 0-1.6.4-3 1-4.3a7 7 0 0 1 3-2.8c1.2-.7 2.7-1 4.3-1 1.7 0 3.2.3 4.4 1a7 7 0 0 1 3 2.8c.6 1.2 1 2.7 1 4.3 0 1.7-.4 3.1-1 4.4a7 7 0 0 1-3 2.8c-1.2.7-2.7 1-4.4 1zm0-3.6c2.4 0 3.6-1.6 3.6-4.6 0-1.5-.3-2.6-1-3.4a3.2 3.2 0 0 0-2.6-1c-2.3 0-3.5 1.4-3.5 4.4 0 3 1.2 4.6 3.5 4.6zm21.7-8.8l-2.7.3c-1.3.2-2.3.5-2.8 1.2-.6.6-.9 1.4-.9 2.5v8.2H96V15.7h4.6v2.6c.8-1.8 2.5-2.8 5-3h1.3l.3 4zm14-3.5h4.8L116.4 37h-4.9l3-6.6-6.4-14.8h5l4 10 4-10zm16-.4c1.4 0 2.6.3 3.6 1 1 .6 1.9 1.6 2.5 2.8.6 1.2.9 2.7.9 4.3 0 1.6-.3 3-1 4.3a6.9 6.9 0 0 1-2.4 2.9c-1 .7-2.2 1-3.6 1-1 0-2-.2-3-.7-.8-.4-1.5-1-2-1.9v2.4h-4.7V8.8h4.8v9c.5-.8 1.2-1.4 2-1.9.9-.4 1.8-.6 3-.6zM135.7 28c1.1 0 2-.4 2.6-1.2.6-.8 1-2 1-3.4 0-1.5-.4-2.5-1-3.3s-1.5-1.1-2.6-1.1-2 .3-2.6 1.1c-.6.8-1 2-1 3.3 0 1.5.4 2.6 1 3.4.6.8 1.5 1.2 2.6 1.2zm18.9 3.6c-1.7 0-3.2-.3-4.4-1a7 7 0 0 1-3-2.8c-.6-1.3-1-2.7-1-4.4 0-1.6.4-3 1-4.3a7 7 0 0 1 3-2.8c1.2-.7 2.7-1 4.4-1 1.6 0 3 .3 4.3 1a7 7 0 0 1 3 2.8c.6 1.2 1 2.7 1 4.3 0 1.7-.4 3.1-1 4.4a7 7 0 0 1-3 2.8c-1.2.7-2.7 1-4.3 1zm0-3.6c2.3 0 3.5-1.6 3.5-4.6 0-1.5-.3-2.6-1-3.4a3.2 3.2 0 0 0-2.5-1c-2.4 0-3.6 1.4-3.6 4.4 0 3 1.2 4.6 3.6 4.6zm18 3.6c-1.7 0-3.2-.3-4.4-1a7 7 0 0 1-3-2.8c-.6-1.3-1-2.7-1-4.4 0-1.6.4-3 1-4.3a7 7 0 0 1 3-2.8c1.2-.7 2.7-1 4.4-1 1.6 0 3 .3 4.4 1a7 7 0 0 1 2.9 2.8c.6 1.2 1 2.7 1 4.3 0 1.7-.4 3.1-1 4.4a7 7 0 0 1-3 2.8c-1.2.7-2.7 1-4.3 1zm0-3.6c2.3 0 3.5-1.6 3.5-4.6 0-1.5-.3-2.6-1-3.4a3.2 3.2 0 0 0-2.5-1c-2.4 0-3.6 1.4-3.6 4.4 0 3 1.2 4.6 3.6 4.6zm27.4 3.4h-6l-6-7v7h-4.8V8.8h4.9v13.6l5.8-6.7h5.7l-6.6 7.5 7 8.2z" fill="currentColor"></path><mask id="b" fill="#fff"><use xlink:href="#a"></use></mask><use fill="#FF4785" fill-rule="nonzero" xlink:href="#a"></use><path d="M23.7 5L24 .2l3.9-.3.1 4.8a.3.3 0 0 1-.5.2L26 3.8l-1.7 1.4a.3.3 0 0 1-.5-.3zm-5 10c0 .9 5.3.5 6 0 0-5.4-2.8-8.2-8-8.2-5.3 0-8.2 2.8-8.2 7.1 0 7.4 10 7.6 10 11.6 0 1.2-.5 1.9-1.8 1.9-1.6 0-2.2-.9-2.1-3.6 0-.6-6.1-.8-6.3 0-.5 6.7 3.7 8.6 8.5 8.6 4.6 0 8.3-2.5 8.3-7 0-7.9-10.2-7.7-10.2-11.6 0-1.6 1.2-1.8 2-1.8.6 0 2 0 1.9 3z" fill="#FFF" fill-rule="nonzero" mask="url(#b)"></path></g></svg>

Hooks<span aria-hidden>🎣</span> or component<span aria-hidden>🧩</span>! You pick!

<!--n--> IntersectionObserver lets us know if the target element is in the viewport or not. If the IntersectionObserver fires, the target element is in the viewport.

<!--v-->

### All-together!

```jsx [|1,2|4|7-9,13|14|12,16]
import React, { lazy, Suspense } from 'react'
import { useInView } from 'react-intersection-observer'

const JustAComponent = lazy(() => import('./JustAComponent'))

const App = () => {
	const { ref, inView } = useInView({
		threshold: 0.0,
	})
	
	return (
		<Suspense fallback={<div>Loading...</div>}>
			<div ref={ref}>
				{inView && <JustAComponent />}
			</div>
		</Suspense>
	)
}
```

<!--n--> From `react-intersection-observer` we use the `useInView` hook, which gives us a `ref` and `inView` flag.<br>
The `ref` should be attached to the target element and `inView` lets us know if the target element is in the viewport.<br>
The threshold option is a value between 0 and 1 indicating the percentage of element that should be visible before triggering.<br><br>
Now, <JustAComponent /> would only be downloaded when it is in the viewport.<br><br>
Demo: https://csb-ceovp.netlify.app/


<!--h-->

## Learnings<!-- .element: data-id="sticky-el-title" -->

- Use this technique with multiple routes or components
<!-- .element: class="fragment" -->

- It can produce easy gains on initial page load times.
<!-- .element: class="fragment" -->

- Not suitable for SSR (or be aware of this when architecting your modules)
<!-- .element: class="fragment" -->

- Use it with SSR to avoid loading chunks in the server
<!-- .element: class="fragment" -->

<!--v-->

## Learnings<!-- .element: data-id="sticky-el-title" -->

- Balance bundle sizes with network requests: network round trip and the latency
<!-- .element: class="fragment" --> 

- We could extract this logic to a wrapper component
<!-- .element: class="fragment" -->

- Take Layout Shifting in consideration<br>
  (and inversion of control if you have a wrapper component)
<!-- .element: class="fragment" -->

- Use skeletons for improved UX and controlled Layout Shifting while loading 
<!-- .element: class="fragment" -->


<!--h-->

## Links

- Dynamic imports: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/import#dynamic_imports
- React.lazy: https://reactjs.org/docs/code-splitting.html#reactlazy
- Skeleton from Material UI: https://material-ui.com/components/skeleton/
- Suspense docs: https://reactjs.org/docs/concurrent-mode-suspense.html

<!--h-->

## Happy conding! 😁👩🏻‍💻
