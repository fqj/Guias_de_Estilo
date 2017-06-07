# Why AMP HTML does not take full advantage of the preload scanner
One of the more controversial design decisions in AMP HTML is that it loads all external resources through custom elements. While this has some benefits (more on that later) it comes with one major problem: The browser’s preload scanner can no longer start downloading those resources very early in the document lifecycle and even worse: the browser needs to download a JavaScript file in order to be able to make those downloads.
The math here is easy: The earlier one starts with resource downloads the earlier they will be around. A very simple document that has a single image on it and nothing else will be much faster if it is not an AMP file.

A very slow scanner that is very unlike the preload scanner. Image: https://commons.wikimedia.org/wiki/File:Drum_scanner.jpg
So, why did AMP HTML disable this super important component of browser speed? — There are 2 primary reasons:

## Reason 1:
The preload scanner’s impact is diminished in AMP
One of its core benefits is that it can start downloading resources before the document’s external stylesheets and synchronous JavaScript files located above the resource in the document hierarchy are downloaded. AMP doesn’t actually allow these, so that benefit goes away.
Additionally, because in AMP HTML the space that will be taken up for an image is always known without downloading it, the effect where a late image can impact page layout is eliminated.

## Reason 2:
 Efficient prerendering[1]
While bare load time is important, AMP aims to support instant loading. This is achieved by prerendering documents. For prerendering an app may download and render a document before a user actually expresses the intent (aka tap, click or press) that they want to see the document. This requires that the app needs to guess which document the user will want to see. Guessing is significantly easier when one gets to make more guesses. In the best case all available documents can be prerendered.
Guessing is significantly easier when one gets to make more guesses.

The main problem with prerendering is that it costs resources: both bandwidth and CPU. AMP HTML supports a special prerender mode for documents where only images are downloaded but no other resources and also only those images that are actually visible when the user first sees the document (aka above the fold). Ignoring CPU for a bit (and it is actually more important but harder to do math with) the following calculation can be done: Say a document typically has 4 large images, but only 1 of those is visible above the fold and download size is dominated by those images (because documents are small), then in AMP prerender-mode the browser can download and prerender 4 documents using the bandwidth that would have been required to prerender a single non-AMP document.
The consequence of this is that apps can prerender AMP HTML documents much more aggressively than they could prerender regular HTML documents.

## Summary
AMP HTML works around the preload scanner because it somewhat paradoxically enables achieving the desired instant load effect. Even if not prerendering, AMP HTML’s document structure significantly offsets the benefits of the preload scanner, so loads are fast even when not prerendering.
[1] “Prerendering” in AMP is referring to an application concept instead of the <link rel=prerender> functionality that is available in some browsers. This may be implemented with a hidden iframe that renders the doc and gets displayed when the user requests it.