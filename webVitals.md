## Getting to Know Web Vitals

In a recent project, my NextJS with Material UI deployment has been loading the initial render slow. So I am learning the debugging process behind that performance lag, which has me getting to know the Web Vitals a bit better. And I thought I'd share what I've learned thus far with you.

I can gain access to the Web Vitals in a few different places, but currently I just want the value output so I'm using the `reportWebVitals` function that is inherit in NextJS and logging them out for quick access, for more detail and suggestions I can run a [Lighthouse](https://developers.google.com/web/tools/lighthouse/) report.

![Lighthouse Performance Report, reading a score of 97 for Ren Estep dot com](images/lighthouse-performance.png)

### Web Vitals

In the simplest terms, Web vitals are useful metrics that help in the examination of the user experience of a webpage. They are an [initiative from Google](https://web.dev/vitals/), that hope to simplify and help focus evaluations to what matters most, these culminate into the **Core Web Values**.

### So what are the **Core Web Values**?

A subset of web vitals that can be applied to all web pages, should be examined and weight by site owners, and have a thread to all the Google tools. The subsets, each has a reference to a specific type of user experience. These references provide measurements and can reflect critical user-centric outcomes.

#### The Core Web Vitals:

- `LCP: Largest Contentful Paint`
- `FID: First Input Delay`
- `CLS: Cumulative Layout Shift`

The metrics listed above are used in measuring important performance elements of user experience, when interacting with a webpage. If you were running a Lighthouse report, the thresholds that are reflected for each metric helps define the performance score for the webpage you're reviewing. Below the Core Web Vitals are expanded upon, along with other metrics that are available through the `reportWebVitals`, which include Web Vitals and NextJS specific metrics.

#### The Web Vitals metrics I have access to through the `reportWebVitals` method:

- `TTFB: Time To First Byte`

  - This metric refers to the time it takes to receive the first byte of information after the browser request it.

- `FCP: First Contentful Paint`

  - The metric reflect the time to the first bit of content rendered to the DOM.
  - This is where a user can start consuming page content.

- **`LCP: Largest Contentful Paint`**

  - This metrics measures loading performance, for "Good UX", loading should take between 0 and 2.5 seconds.
  - Using the `reportWebVitals`, the value is represented in milliseconds

- **`FID: First Input Delay`**

  - A metric for measuring Load responsiveness, when this number is low the site is typically easier to use and navigate.
    - The perception of the end user's experience while interacting with the web page.
  - It help measure the time from when the user first interacts with the page to the time when the browser processes the interaction.
  - For "Good UX", that time should fall between 0 and 100 milliseconds

- **`CLS: Cumulative Layout Shift`**
  - A metric for measuring visual stability.
  - This measures the largest burst of layout shifts that are unexpected through out the life of a page.

#### Additional NextJS Specific Metrics:

- `Next.js-hydration`

  - This measures the length of time from start to finish, it takes a page to Hydrate in milliseconds.
  - What is Hydration?
    - The process of attaching react listeners to HTML-DOM nodes.
    - Rehydration is basically the same, but in reference to Server Side Rendered(SSR) rendered HTML. The listeners still need to be attached.

- `Next.js-route-change-to-render`

  - How long it takes a page to start rendering after a route change.
  - It is measured in Milliseconds.

- `Next.js-render`

  - How long it takes a page to finish rendering after a route change.
  - It is measured in Milliseconds.

### Thoughts on improving the **Core Web Values**

- `LCP: Largest Contentful Paint`

  - Remove unnecessary 3rd part scripts
  - Set up Lazy or Dynamic loading, Loading components only when they are needed
  - Remove large page elements
  - Minify your CSS
  - Upgrade your hosting

- `FID: First Input Delay`

  - Minimize JavaScript, page interactions are slowed down if the page is loading javascript.
  - Remove any unnecessary 3rd party scripts
  - Use a browser caching

- `CLS: Cumulative Layout Shift`
  - Set size attributes for any medias types
  - Ads should have reserved space, placeholders
  - Adding new UI elements should happen in a way that they don't unexpectedly push content down or over.
    - Avoid content shifting around the page.
    - Dynamically/ lazy load components

I'm in the process of testing out different solutions, for my larger numbers. I'm looking at rendering a static page initially, fingers crossed it's the first solution (_we all know it never is_)! It's been a joy learning as new development opportunities that have come with bigger responsibilities. I hope my notes help on your learning path as well.

## Resources

- [Web.dev Web Vitals](https://web.dev/vitals/)
- [BACKLINKO User Experience Signals: Core Web Vitals](https://backlinko.com/hub/seo/core-web-vitals)
- [NextJS Web Vitals](https://nextjs.org/docs/advanced-features/measuring-performance#build-your-own)
- [NextJs Learn: Improving Your Core Web Vitals](https://nextjs.org/learn/seo/improve)
