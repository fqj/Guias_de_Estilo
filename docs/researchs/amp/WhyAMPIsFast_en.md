# Why AMP is fast
The AMP Project aims to bring instant rendering to web content. This is an unsorted list of optimizations that apply to all AMP based documents, which in aggregate makes them load fast. Every web page can have these optimizations, but AMP pages cannot not have them.
While this article is about optimizations in AMP, it might also be useful as a kind of todo list for optimizing a non-AMP website. If we are missing any optimization that might be benifitial to AMP, please leave a comment or send us a pull request.

## Lazy loading
Resources are lazy loaded when it becomes likely that they’ll be seen by the user or when the document is otherwise idle.

## Extensive use of preconnect
The new preconnect API is used heavily to ensure HTTP requests are as fast as possible when they are made. This helps makes lazy loaded requests faster when they are eventually made.

## Prefetching of lazy loaded resources
Resources are loaded as late as possible, but prefetched as early as possible. That way things load very fast but CPU is only used when resources are actually shown to users.

## All async JavaScript
AMP files are only valid if all JavaScript files are loaded asynchronously.

## Inline style sheets
Only inline style sheets are allowed in AMP. This removes 1 or often more HTTP requests from the critical rendering path compared to most web pages.

## Zero HTTP requests block font downloads.
Because all JS in AMP has the async attribute and only inline style sheets are allowed, no HTTP requests block the browser from downloading fonts.

## Instant loading through prerendering
AMP is optimized for making it relatively “cheap” and reliable to prerender a resource. This means that it is rendered before the user explicitly states that they’d like to navigate to a page. With this a page might already be available by the time the user actually selects it, leading to instant loading.
While prerendering can be applied to all web content, that may (and does in practice) use up a lot of bandwidth and CPU. AMP is optimized to reduce both of these factors:

## Prerendering only downloads resources above the fold
When AMP documents get prerendered for instant loading, only resources above the fold are actually downloaded. Details.
Prerendering does not render things that might be expensive in terms of CPU
When AMP documents get prerendered for instant loading, resources that might use a lot of CPU (like third party iframes) do not get downloaded. Details.

## Intelligent resource prioritization
When AMP downloads resources it optimizes downloads so that those resources that are currently most important for the user are downloaded first.

## Uncoupling of document layout from resource downloads
External resources such as images, ads or iframes need to state their size in the HTML. That means they don’t have to be downloaded first to layout the document.

## Maximum size for style sheet
The inline style sheet has a maximum size. While this size is big enough for very sophisticated pages, it still requires the page author to practice good CSS hygiene.

## FastDOM-style DOM change batching
We batch all DOM measure and mutate operations to minimize style recalculations in the browsers.
In practice this means that in each “animation frame” we first do all the DOM read operations, and then when those are done, do all the write operations. The result is a reduction to 1 style recalculation per frame.

## Optimized for low count of style recalculations and layout
Independent of the above, AMP is optimized to avoid expensive style recalculations and layouts in the browser.

## Mitigations for third party JS worst-practices such as document.write
In particular if third party JS uses the super-bad-for-performance “document.write” API, it does not block rendering the main page.

## Runtime cost of analytics instrumentation is independent of number of used analytics providers
The way analytics are being implemented in AMP, pages that have more than one analytics provider do not get bloated with additional JavaScript and do not use significant extra CPU.

## Extensions don’t block page layout
AMP supports extensions for things like lightboxes, instagram embeds, tweets, etc. While these require additional HTTP requests, those requests do not block page layout and rendering.

## CDN delivery available to all AMP documents
AMP offers a proxy-based CDN for delivering all valid AMP documents, offering fast and reliable performance across all AMP content.

All resources and the document are loaded from the same origin through the same HTTP 2.0 tunnel
When using the proxy-based AMP CDN, the document, all JS files and all images are loaded from the same origin that is using HTTP 2.0 for maximum efficiency.

## Animations can be GPU accelerated
The rules for animation related CSS in AMP ensure that animations can be GPU accelerated on modern devices, so they are smooth and buttery.