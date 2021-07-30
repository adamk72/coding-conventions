**A note to the reader:** This is currently in a state of flux, created in an ad-hoc manner from several recent projects coming to a head. I will be collborating with those folks and others to implement a better, more comprehensive version of this ReadMe file for the wider community.

# Coding Conventions

Use these rule for Guidance:

- [C^3: Common Coding Conventions](https://github.com/tum-esi/common-coding-conventions)
- [React Thinking](https://reactjs.org/docs/thinking-in-react.html)

🥇 Golden Rule: Don't Repeat Yourself (DRY). - Corollary #1: This applies to CCS classes as well. - Corollary #2: Code duplication can be subtle. Keep the big picture in mind.

🥈 Silver Rule: Favor composition over procedure.

🥉 Bronze Rule: If the only difference in a code block is a variable, make the code block a component and pass in that variable as a parameter. - Corollary: Multiple parameters can be a single object and thus a single parameter.

👌 Okay Rule: It's okay to pull code out as a one use component if it help improve readability.

# **Code Observations**

## Basics

**Long files**

- If it's over 200 lines long, consider breaking it up.

**Colors**

- Direct colors like pink, blue, or even buttonPink should not be referred to directly in code. Colors only appear in stylesheets.
- https://tailwindcss.com/docs/customizing-colors
- Should be in tailwind.config.js or a root node.

```
/* In your CSS */
:root {
  --color-primary: #5c6ac4;
  --color-secondary: #ecc94b;
  /* ... */
}

@tailwind base;
@tailwind components;
@tailwind utilities;
```

**Code formatting**

- Install Prettier

**Breakpoints**

- https://tailwindcss.com/docs/breakpoints

**Hard Coding**

- Remove **ALL** hard coding values, even if they seem "obvious"
  - All values should have a name
  - Chances are, Tailwind or other framework for what is needed.

**Lists**

- If it looks like list, it is list:
  - Abstract all list items to a main component.
  - Create an array of of object to pass as parameters.
  - There are no exceptional cases for a list item. They're all the same at some root level if you look deep enough.

## Slightly More Advanced

**Control Structures**

- Ternary expressions should be very short and very readable.
  - If you can't keep track of the logic, it's too complex.
- Try not to use `else`.
  - Complex `if` and `switch` statements can often be replaced by the judicious use of an well planned array or object which expands later options.

## CSS

**Colors, again**

- Remove hard code hex values. Use CSS variable in all cases.
  - Except white or black, since they are easy to search for.

**Duplication of CSS Strings**

- If you keep repeating the same classes over and over, that means they are their own class.
- In Tailwind, use `@apply`.

**Tailwind**

- [Function & Directives](https://tailwindcss.com/docs/functions-and-directives)
- [Responsive Design](https://tailwindcss.com/docs/responsive-design)

**Grommet**

- This is lightweight and highly customizable: [Grommet](https://v2.grommet.io/components)

## HTML Tags

- `<div>`

  - Do not nest these (or any tag) too deeply.
  - Apply the Bronze Rule when you get more the 3 layer deep

- `<span>`

  - use this sparingly
  - Use `div` and a CSS class that uses `display: inline` (if needed)
  - Use a specific element, like `<em>` instead or write a component

- `<button>`
  - Better to make this a component if it has special characteristics

## Questions

- Why is `onWindowSizeChange` copied in multiple place? Either:

  - Create a hook for it
    - Why is it checking for a change in screen size at all?
    - Remove hard coded values (1024, 768)
    - isMobile, isTablet is poor practice
  - Or better, let Tailwind handle that decision.
