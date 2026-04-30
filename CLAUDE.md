# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page marketing site for the Exodus iGaming Platform. Pure static HTML/CSS — no JavaScript framework, no build step, no package manager, no tests. The CTAs link to a Calendly booking URL.

## Working on it

There is nothing to install or compile. To preview changes, open `index.html` directly in a browser, or serve the directory (e.g. `python3 -m http.server` from the repo root). Refresh after editing.

All page content lives in `index.html`. All styling lives in `assets/css/style.css`. Images (mostly `.webp`, plus the SVG logo) live in `assets/images/`.

## Page structure

The page is a `<header>` followed by a `.container` holding eight numbered sections (`one-section` through `eight-section`) plus a logo slider and a footer-positioned `.exodus` background. Section numbering in the HTML, CSS class names, and the matching `section-N.webp` image files are aligned — when adding or reordering sections, keep these three in sync.

Reused patterns to know before editing CSS:

- `.blur-section` is the styled card used by sections one/two/three/five. Its gradient "orb" glows are rendered via `::before` and `::after` pseudo-elements — don't repurpose those without checking the visual.
- Inside each `.blur-section`, a child `<div class="section-element">` is the layer that holds the section-specific decorative background image. The image, sizing, and positioning are set per-section in `style.css`.
- The header gets its main-bg from `header { background-image: url(../images/main-bg.webp) }`; the `.header-bottom` div underneath layers `header-bottom.webp` plus a fade-to-page-color gradient via `::after`.
- The logo carousel (`.six-section`) achieves seamless infinite scroll by duplicating the `.logo-slider-wrapper` block in the HTML and animating the parent `.logo-slider-container` with the `moveSlideshow` keyframes (translateX -50%). Both wrappers must stay identical or the loop will jump.
- `h1`/`h2`/`.specification-title` use a white-to-grey gradient via `background-clip: text` — set color through `background-image`, not `color`.

## Responsive breakpoints

Layout adapts at four widths: `1280px`, `1024px`, `768px`, and `480px`. The mobile nav (`<nav>`) is hidden below 768px, and below 480px the `.blur-section` cards switch to a stacked layout with the decorative image moved to the top (`padding-top: 280px`, `background-position: top center`). Test changes at all four breakpoints.

## Third-party embeds

The bottom of `<body>` in `index.html` contains Google Ads (`gtag.js`, conversion ID `AW-16689451104` / send-to `AW-16651553142/...`) and the Meta Pixel (`fbq`, ID `2390507621297467`). These are tracking scripts — leave them in place when editing the page unless explicitly asked to remove them, and avoid moving them above page content.
