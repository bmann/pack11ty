---
title: CSS and JavaScript assets
---

Both CSS and JavaScript are split (manually) in two parts:

- one **critical** for performance is included inline in all HTML pages
- one additional, less important for performance, is loaded in the end of the HTML, with a hash to prevent caching issues

# JavaScript

Additional JavaScript is loaded as [ECMAScript module](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/) in modern browsers, and as [Immediately Invoked Function Expression](https://en.wikipedia.org/wiki/Immediately_invoked_function_expression) (IIFE) in older ones, using the `module`/`nomodule` pattern for [differential serving](https://css-tricks.com/differential-serving/)[^modules].

[^modules]: You can watch [this hilarious video](https://www.youtube.com/watch?v=dAIckpwW9ds) by Heydon Pickering, about ES modules, for a few minutes of fun.

JavaScript is compiled with [Rollup](https://rollupjs.org/), with a few plugins:

- `babel` for transpiling to ES5 where necessary
- `terser` for minification

# CSS

CSS is compiled from [Sass](https://sass-lang.com/) code, also with Rollup, thanks to the [rollup-plugin-scss](https://github.com/thgh/rollup-plugin-scss) plugin.

Critical and additional CSS are thus a little tied to their JavaScript counterparts, which are entries for Rollup. Not ideal, but it allows using one single bundler.

The Rollup configuration for CSS also includes generation of a hashed filename for cache busting.

::: info
[Pack11ty]{.pack11ty} initialy used `postcss` and a few plugins to generate CSS, but it was not as complete as full Sass, and the npm scripts were a mess. Look at [the Pull Request that changed this to Rollup and Sass](https://github.com/nhoizey/pack11ty/pull/13) if you want to compare.
:::

# Dev mode with Live Reload

_WIP_
