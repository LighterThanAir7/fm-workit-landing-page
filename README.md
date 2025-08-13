# Frontend Mentor - Workit landing page solution

This is a solution to the [Workit landing page challenge on Frontend Mentor](https://www.frontendmentor.io/challenges/workit-landing-page-2fYnyle5lu). Frontend Mentor challenges help you improve your coding skills by building realistic projects.

## Table of contents

- [Overview](#overview)
  - [The challenge](#the-challenge)
  - [Screenshot](#screenshot)
  - [Links](#links)
- [My process](#my-process)
  - [Built with](#built-with)
  - [What I learned](#what-i-learned)
  - [Continued development](#continued-development)
  - [Useful resources](#useful-resources)
- [Author](#author)

## Overview
### The challenge

Users should be able to:
- Implement given design using HTML and CSS to get the same result as in the design file respecting responsive design

### Screenshot

![](./screenshot.avif)

### Links

- Solution URL: [Github Repo](https://github.com/LighterThanAir7/fm-workit-landing-page)
- Live Site URL: [Github.io](https://lighterthanair7.github.io/fm-workit-landing-page)

## My Process

### Built with

- Semantic HTML5 markup
- SCSS preprocessor
- Desktop-first workflow

### What I learned

I learned to convert SVG section-divider shapes to a relative coordinate system, which makes them scale more elegantly and improves responsiveness. I also used [Axe DevTools](https://www.deque.com/axe/devtools/) to audit accessibility and realized how important a proper heading hierarchy is. Jumping from an h1 directly to an h3 isn’t ideal, so I added an h2 for the “values” section using an sr-only utility class to keep the semantics correct without changing the visual design.

Here are two small snippets I’m proud of from this project.
1) Using native CSS counters instead of extra <span> elements for the values section:

```scss
.value {
    @include flex($g: size(32));
    counter-reset: counter;
    padding-top: size(88);
    padding-bottom: size(144);

    &__item {
        counter-increment: counter;
        position: relative;
        text-align: center;

        &::before {
            @include flex($ai: center, $jc: center);
            content: counter(counter);
            width: size(56);
            height: size(56);
            border-radius: 50%;
            color: clr(purple, 900);
            outline: 1px solid clr(purple, 500);
            margin-inline: auto;
            margin-bottom: size(64);
            font-family: $ff-primary;
            font-size: 1.5rem;
            line-height: 2.5rem;
        }

        // ...
    }
    
    // ...
}

```

2) Dynamically calculating an offset for responsive positioning of hero decorative elements:

```scss
.hero {

    // ...
    &__decoration {
        position: absolute;
        top: calc(#{size(56)} + var(--offset));

        &-left {
            --offset: 47px;
            $max_vw: 1440px;
            $min_vw: 768px;

            $left_start: -20px;
            $left_end: -220px;

            $delta_left: $left_end - ($left_start);
            $delta_vw: $min_vw - $max_vw;

            $multiplier: ($delta_left / $delta_vw);
            $multiplier_vw: $multiplier * 100vw;

            $fixed_value: $left_start - ($max_vw * $multiplier);
            left: clamp($left_end, $multiplier_vw + $fixed_value, $left_start);
        }

        // ...
    }

    // ...
}
```

### Continued development

Here are the areas I want to keep focusing on:
- I’m relatively new to web accessibility and I’m working toward meeting WCAG 2.2 AA.
- Skip-to-main-content: adding a visible-on-focus skip link and ensuring the main region can receive programmatic focus.
- ARIA usage: prefer native HTML semantics first; add ARIA only when necessary. Learn where aria-label/aria-labelledby/aria-describedby are appropriate, and avoid redundant or conflicting ARIA.
- Roles and landmarks: use semantic elements (main, header, nav, footer, aside) before adding role attributes; apply roles to fill gaps only when there’s no suitable native element.
- Headings and document outline: maintain a logical hierarchy (h1 → h2 → h3…). In cases where a visual design skips a level, supply an appropriate heading for semantics (e.g., an off-screen “sr-only” h2) while keeping the visual design intact.
- Keyboard accessibility: ensure all interactive elements are reachable and operable via keyboard, with clear focus states and no keyboard traps.

### Useful resources

- [Using CSS counters](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_counter_styles/Using_CSS_counters) - This helped me utilize native CSS counters to auto-number elements without adding extra markup like dedicated <span> or <div> with hardcoded numbers. I really liked this pattern and will use it going forward.
- [Convert SVG absolute clip-path to relative](https://yoksel.github.io/relative-clip-path/) - This helped me take the custom section divider shape from Figma and convert its SVG coordinates from absolute to relative for easier responsiveness. A very handy tool.

## Author

- Github - [LighterThanAir7](https://github.com/LighterThanAir7)
- Frontend Mentor - [@LighterThanAir7](https://www.frontendmentor.io/profile/LighterThanAir7)