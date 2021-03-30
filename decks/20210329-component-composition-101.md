---
title: Component Composition 101
date: 29.03.2021
author: Manuel Lieb
description: The Art of Nesting
separator: "^\r?\n---\r?\n$"
verticalSeparator: "^\r?\n   ---\r?\n$"
theme: black
css: ./custom/styles/general.css
template: ./custom/templates/general.html
highlightTheme: monokai
---

## Component Composition 101

The Art of Nesting

---

### Why should you care? 🤔

- Prevents (excessive) Prop-Drilling
- Makes your code more readable / extensible
- Improves re-usability of Components
- Enables customisable placements inside your Components

Notes:
Can be an alternative to Context, depending on the Use-Case
Customisation can lead to other Problems, but still could be beneficial depending on the use-case

---

### You right now ...

![You right now in Front of the Screen - puking rainbows](assets/20210329/rainbow-puke.gif)

---

### Meet your Enemy

[Codesandbox](https://codesandbox.io/s/component-composition-demo-82heq?file=/src/examples/prop-drilling/prop-drilling.tsx)

---

### Basic Composition

Utilize the `children` prop to pass a Component into another Component

Note: in Vue / Svelte the default children Prop is <slot />

   ---

![Demo Time - Spongebob](assets/20210329/demotime1.jpg)

[Codesandbox](https://codesandbox.io/s/component-composition-demo-82heq?file=/src/examples/prop-drilling/prop-drilling.tsx)

---

### Advanced Composition (-Patterns)

Your Composition can be enhanced using:

- Functions as Child Component (FaCC)
- renderProps
- Component Injection

---

### Functions as Child Component (FaCC)

Same pattern as using `children` - but instead of a Component you pass a function.

Inside the Component you call the `children()` function and optionally return the defined values.

Note: using FaCCs is the easiest but also most controversial Composition Pattern

   ---

#### Component

```tsx[1-7]
const Switch = ({ children }: SwitchProps) => {
	const [isActive, setIsActive] = useState<boolean>(false);
    
    // ...
    
	return children(isActive);
};

type SwitchChildProps = {
	isActive: boolean;
}

type SwitchProps = {
	children?: FunctionComponent<SwitchChildProps>
}
```

#### Usage

```tsx
<Switch>
   {(isActive) => <button>{isActive ? 'Disable' : 'Activate'}</button>}
</Switch>
```

---

### renderProps

Instead of using the `children` prop, you define a dedicated prop for the rendering.

Using renderProps you can define multiple "slots" which can be rendered at a specific place inside the Component.

Note: in Vue / Svelte you can give Slots a name

   ---

#### Component

```jsx[1-11]
const NewsDetail = ({ id, author, comments }: NewsDetailProps) => {
   const [authorId, setAuthorId] = useState<number>(1)

   return (
      <>
         {author(authorId)}
         // render news content here
         {comments(id)}
      </>
   );
};

type NewsDetailProps = {
	author?: FunctionComponent<AuthorProps>
	comments?: FunctionComponent<CommentsProps>
}
```

#### Usage

```jsx
<NewsDetail
  id={123}
  author={(authorId) => <Author id={authorId} />}
  comments={(newsId) => <Comments id={newsId} />}
/>
```

---

### Component Injection

Instead of passing a function - you can also directly pass a Component - to render.

This is pretty handy, if you don't need to rely on any data from the parent Component.

   ---

#### Component

```tsx[1-8]
const Input = ({ inputRightIcon: IconRightRender, ...rest }: InputProps) => {
   return (
      <label>
        <input {...rest} />
        {inputRightIcon && <IconRightRender />}
      </label>
   );
};

type InputProps = {
   inputProps?: HTMLInputElement;
   inputRightIcon?: ReactNode;
}
```

#### Usage

```tsx
<Input
  type="text"
  name="username"
  inputRightIcon={<Icon name="user" />}
/>
```

---

### Bonus: Some Magic ✨

Allow passing a Component or Function in the same Component

```tsx
const Switch = ({ children }: SwitchProps) => {
	const [isActive, setIsActive] = useState<boolean>(false);

	return isFunction(children) ? children(isActive) : children;
};

type MaybeRenderProp = ReactNode | FunctionComponent<P>;

type SwitchChildProps = {
	isActive: boolean;
}

type SwitchProps = {
	children?: FunctionComponent<SwitchChildProps>
}

function isFunction(value: any): value is Function {
	return typeof value === "function"
}
```

---

### Questions?

![Next Talk](assets/20210329/questions.gif)

---

### Nomination

   ---

![Next Talk](assets/20210329/next-talk.jpg)

---

### Sources:

* [Function as Child Components Are an Anti-Pattern](https://americanexpress.io/faccs-are-an-antipattern/)
* [Using Composition in React to Avoid "Prop Drilling"](https://www.youtube.com/watch?v=3XaXKiXtNjw)
