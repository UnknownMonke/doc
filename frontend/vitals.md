# Core Web Vitals

### Summary

- [Motivations](#Motivations)
- [Web Vitals](#web-vitals)
    - [Associated Tools](#associated-tools)
- [Structure](#structure)
- [Largest Contentful Paint (LCP)](#largest-contentful-paint-lcp)
    - [Optimizations](#optimizations)
- [First Input Delay (FID)](#first-input-delay-fid)
- [Interaction to Next Paint (INP)](#interaction-to-next-paint-inp)
- [Cumulative Layout Shift (CLS)](#cumulative-layout-shift-cls)
    - [Optimizations](#optimizations)
- [First Contentful Paint (FCP)](#first-contentful-paint-fcp)
    - [Optimizations](#optimizations)
- [Time to first byte (TTFB)](#time-to-first-byte-ttfb)
- [Total blocking time](#total-blocking-time)
- [Accessibility](#accessibility)
    - [Optimizations](#optimizations)
- [Search Engine Optimization (SEO)](#search-engine-optimization-seo)
    - [Optimizations](#optimizations)
- [Various Optimizations](#various-optimizations)
- [Continous Monitoring and Optimization](#continous-monitoring-and-optimization)

#
> [Official Google Knowledge Base](https://web.dev/explore/learn-core-web-vitals).

<br>

## Motivations

- Website performance directly impacts user experience :

    - Poor **responsiveness**.
    - Slow **loading times**.

- Also impacts **Search Engine Optimization** (**SEO**).

<br>

## Web Vitals

- Initiative by Google to provide <u>unified guidance</u> through **quality signals** for websites :

    - Performance.
    - Accessibility.
    - Best practices.
    - SEO.
    - Progressive Web App.

- Provides a set of **metrics** for each categories.

<br>

> Maintained and *updated*, Google knowledge base should be regularly checked.

#
### Associated Tools

- **Google Lighthouse**

    - Chrome console tab that generates a **report** about performances & best practices.
    - Current url only.
    - Open source.

- [**PageSpeed Insights**](https://pagespeed.web.dev/)

    - Built by Google.
    - Uses lighthouse under the hood.
    - More powerful :
        - Side-by-side view for mobile and desktop.
        - Collects data from multiple users sessions and builds averages.
    - Still limited to a single url.

- [**Google Search Console**](https://search.google.com/search-console/about)

    - More powerful than PageSpeed :
        - Can generate reports and overviews for all urls of a web app.

- [**GTMetrix**](https://gtmetrix.com/)

    - Automatic monitoring tasks.
    - History graphs of performances.

<br>

## Structure

**<u>Core Web Vitals</u>** :

Set of most essential metrics to deliver a great user experience for a majority of users.

- **Largest Contentful Paint (LCP)**.
- **First Input Delay (FID)**.
- **Interaction to Next Paint (INP)**.
- **Cumulative Layout Shift (CLS)**.

<br>

**<u>Other Metrics</u>** :

Some less critical yet not less important metrics.

- **First Contentful Paint (FCP)**.
- **Time to first byte (TTFB)**.
- **Total blocking time**.

<br>

**<u>Accessibility</u>**.

**<u>Search Engine Optimization (SEO)</u>**.

<br>

## Largest Contentful Paint (LCP)

- Render time of the *largest image or text block* visible *within the viewport*, relative to the first navigation to the page.

- Can happen before the page is fully loaded, if the largest element is loaded in early.

#
### Optimizations

- Use efficient **cache policy**.

- Serve images in better compressed formats (**webP**).

- Additional use of *tinypng.com* to further compress without losing quality.

- Crop images to remove unused parts when possible, reducing dimensions & size.

- No oversized images relative to screen size : images size should not be bigger than screen size at least.

- Do not load images or resources for multiple screen sizes at once, only the necessary resources should be loaded for the **current screen size**.

    ``` html
    <picture>
        <!-- Matches the first source found. -->
        <source media="(max-width: 576px)" srcset="img/hero_mobile.webp">
        <source media="(max-width: 960px)" srcset="img/hero_tablet.webp">
        <img src="img/hero_desktop.webp">
    </picture>
    ```
<br>

## First Input Delay (FID)

> Deprecated.

- Time from the first user interaction with a page, to when the browser is able to process the event handler.

- Can be affected by loading time, poor connectivity and blocking actions.

<br>

*Ex :* 

Clicking on a menu while the page have not finished loading will delay the input processing, resulting in waiting time from the user.

<br>

## Interaction to Next Paint (INP)

- Time of the interaction or the average interaction with the worst latency among all page interactions.

- Unlike FID, does not focus on first delat but delay throughout the subsequent navigations.

<br>

## Cumulative Layout Shift (CLS)

- Measures **unexpected layout shifts** occurring during the entire lifespan of the page.

- **Layout shift** : A visible element changes its position from one redered frame to the next.

- Unexpected movement of page can happen when :

    - Resources are loaded **asynchronously**.
    - DOM elements are *dynamically* added.

- May result in missclicks from users when elements they want to click on suddenly move.

<br>

*Ex :*

- Font rendering larger or smaller than its fallback.
- Ad or third-party content popping.
- Image or video with unknown dimension.

#
### Optimizations

- Reserve space for images to load in a container with their dimension, so no shifting occurs : `width` and `height` attributes set.

- Set `max-width: 100%` to avoid overflow.

- For dynamically loaded images where specific dimensions are not known, **lazy-loading** would be enough.

- For other elements :

    - Use **opacity** instead of display to reserve space (blank space).
    - **Fixed height or width container**.

- Self host google fonts to avoid font fallback.

<br>

## First Contentful Paint (FCP)

- Time when the first element become visible.

#
### Optimizations

- **Lazy-load** offscreen images.

    - Use the `loading="lazy"` attribute to enable **native** lazy-loading in the browser.

- Avoid **render-blocking resources** (fonts, third-party scripts...) necessary to correctly load the page.

- Reduce execution time for client loading and processing (API calls, JS processing).

    - Lazy-loading offscreen content on scroll.
    - Web workers.
    - Async tasks.
    - Use **hooks** (`window.onload`, `document.DOMContentLoaded`...).

- Defer `<script>` tags.

- Be careful when lazy-loading as this can create **latency** during interactions as content is dynamically loaded, increasing **INP**.

<br>

## Time to first byte (TTFB)

- Time between the request for a resource and when the **first response byte** starts to arrive.

- Fondamental in measuring **connection** setup time and web server **responsiveness**.

<br>

> If a server is slow to load HTML, every other metric becomes **irrelevant**.

<br>

## Total blocking time

- Total amount of time after FCP where the main thread was blocked for long enough to prevent input responsiveness.

<br>

*Ex :*

- Async JS files.
- Exessive DOM size.

<br>

## Accessibility

- Specifies **attributes** and **aliases** for *screen readers* towards visually impaired people.

#
### Optimizations

- `aria` attributes on DOM elements.

- `alt` attribute on images.

    - Unimportant images should have an empty alt.

- **High contrast ratio** between colors (can be calculated online).

<br>

## Search Engine Optimization (SEO)

- Techniques to increase the site's visibility in searches results.

#
### Optimizations

- Add a meta description for search engines.

``` html
<head>
    <meta name="description" content="My website description to appear in the search results.">
</head>
```
<br>

## Various Optimizations

- **Keep image aspect ratio** : a `max-width` or `max-height` css property should be followed by a `height : auto` or `width : auto`.

<br>

## Continous Monitoring and Optimization

- Define and enforce **best practices**.

    - Training for newcomers.
    - Keep an eye for new practices.
    - Write a Best Practices cheatsheet or checklist.

- **Monitor performances** with tools, set up alerts.

    - PageSpeed.
    - Google Search Console.
    - GTMetrix.
    - ...

- **Allocate resources**.

    - Code reviews.
    - Create QA processes.