# Global Styles

The **global.css** file in the `app/` directory of a next.js project is usually used for styles that are truly global in the application. (Styles that apply on all pages).

Custom classes should not be defined here as they only apply to a certain page or component. Moreover, as the project grows the global.css file becomes really large and unmaintainable.

It is best practice when performing initial cleanup of the file to have it as follows:

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  --foreground-rgb: 0, 0, 0;
}

@media (prefers-color-scheme: dark) {
  :root {
    --foreground-rgb: 255, 255, 255;
  }
}

```