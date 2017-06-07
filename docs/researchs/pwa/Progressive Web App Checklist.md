# Progressive Web App Checklist

Progressive Web Apps (PWA) are reliable, fast, and engaging, although there are many things that can take a PWA from a baseline to exemplary experience.

To help teams create the best possible experiences we've put together this checklist which breaks down all the things we think it takes to be a Baseline PWA, and how to take that a step further with an Exemplary PWA by providing a more meaningful offline experience, reaching interactive even faster and taking care of many more important details.

# Baseline Progressive Web App Checklist

The [Lighthouse tool](https://chrome.google.com/webstore/detail/lighthouse/blipmdconlkpinefehnmjammfjpmpbjk) is able to automatically verify many items on the this list and may prove helpful in easily testing sites.

# Site is served over HTTPS

To Test:	Use Lighthouse to verify Served over HTTPS
To Fix: 	Implement HTTPS and check out letsencrypt.org to get started.

# Pages are responsive on tablets & mobile devices

To Test	: * Use Lighthouse to verify Yes to all of Design is mobile-friendly, although manually checking can also be helpful.
* Check the Mobile Friendly Test
To Fix	Look at implementing a responsive design, or adaptively serving a viewport-friendly site.

# The start URL (at least) loads while offline

To Test:	Use Lighthouse to verify URL responds with a 200 when offline.
To Fix:	Use a Service Worker.

# Metadata provided for Add to Home screen

To Test:	Use Lighthouse to verify User can be prompted to Add to Home screen is all Yes.
To Fix:	Add a Web App Manifest file to your project.

# First load fast even on 3G

To Test:	Use Lighthouse on a Nexus 5 (or similar) to verify time to interactive <10s for first visit on a simulated 3G network.
To Fix:	
* There are many ways to improve performance.
* You can understand your performance better by using Pagespeed Insights (aim for score >85) and SpeedIndex on WebPageTest (aim for <4000 first view on Mobile 3G Nexus 5 Chrome)
* A few tips are to focus on loading less script, make sure as much script is loaded asynchronously as possible using <script async> and make sure render blocking CSS is marked as such.
* You can also look into using the PRPL pattern and tools like PageSpeed Module on the server.

# Site works cross-browser
To Test:	Test site in Chrome, Edge, Firefox and Safari
To Fix:	Fix issues that occur when running the app cross-browser

# Page transitions don't feel like they block on the network
Transitions should feel snappy as you tap around, even on a slow network, a key to perceived performance.
To Test:	Open the app on a simulated very slow network. Every time you tap a link/button in the app the page should respond immediately, either by:
* Transitioning immediately to the next screen and showing a placeholder loading screen while waiting for content from the network.
* A loading indicator is shown while the app waits for a response from the network.
To Fix:	If using a single-page-app (client rendered), transition the user to the next page immediately and show a skeleton screen and use any content such as title or thumbnail already available while content loads.

# Each page has a URL
To Test:	Ensure individual pages are deep linkable via the URLs and that URLs are unique for the purpose of shareability on social media by testing with individual pages can be opened and directly accessed via new browser windows.
To Fix:	If building a single-page app, make sure the client-side router can re-construct app state from a given URL.

# Exemplary Progressive Web App Checklist

Many of these checks must be performed manually, as they are not yet implemented in Lighthouse.

Indexability & social

For more information, see our guide to social optimization and social discovery.

# Site's content is indexed by Google
To Test	Use the Fetch as Google tool to preview how Google will see your site when it is crawled.
To Fix	Google's indexing system does run JavaScript but some issues may need to be fixed to make content accessible. For example, if you are using new browser features like the Fetch API, ensure that they are polyfilled in browsers without support.
Schema.org metadata is provided where appropriate
Schema.org metadata can help improve the appearance of your site in search engines.
To Test	Use the testing tool to ensure title, image, description etc. are available.
To Fix	Markup the content. For example:
A recipe app should have the Recipe type markup for Rich Cards.
A news app should have the NewsArticle type markup for Rich Cards and/or AMP support.
An ecommerce app should have the Product type markup for Rich Cards.

# Social metadata is provided where appropriate
To Test	
Open a representative page in Facebook's crawler and ensure it looks reasonable.
Check that Twitter Cards meta data is present (for example <meta name="twitter:card" content="summary" />) if you feel it would be appropriate.
To Fix	Mark up content with Open Graph tags and as advised by Twitter.

# Canonical URLs are provided when necessary
This is only necessary if your content is available at multiple URLs.
To Test	
Determine whether any piece of content is available at two different URLs.
Open both of these pages and ensure they use <link rel=canonical> tags in the head to indicate the canonical version
To Fix	Add a canonical link tag to the <head> of each page, pointing to the canonical source document. See Use canonical URLs for more information.

## Pages use the History API
To Test	For single page apps, ensure the site doesn't use fragment identifiers. For example everything after the #! in https://example.com/#!user/26601.
To Fix	Use the History API instead of page fragments.

# User experience

## Content doesn't jump as the page loads
To Test	Load various pages in the PWA and ensure content or UI doesn't "jump" as the page loads.
To Fix	Ensure all content, especially images and ads, have fixed sizing in CSS or inline on the element. Before the image loads you may want to show a grey square or blurred/small version (if available) as a placeholder.

## Pressing back from a detail page retains scroll position on the previous list page
To Test	Find a list view in the app. Scroll down. Tap an item to enter the detail page. Scroll around on the detail page. Press back and ensure the list view is scrolled to the same place it was at before the detail link/button was tapped.
To Fix	Restore the scroll position in lists when the user presses 'back'. Some routing libraries have a feature to do this for you.

## When tapped, inputs aren't obscured by the on screen keyboard
To Test	Find a page with text inputs. Scroll to put the text input as low on the screen as you can make it. Tap the input and verify it is not covered when the keyboard appears.
To Fix	Explore using features like Element.scrollIntoView() and Element.scrollIntoViewIfNeeded() to ensure the input is visible when tapped.

## Content is easily sharable from standalone or full screen mode
To Test	Ensure from standalone mode (after adding the app to your home screen) that you are able to share content, if appropriate, from within the app's UI.
To Fix	Provide social share buttons, or a generic share button within your UI. If a generic button, you may want to directly copy the URL to the user's clipboard when tapped, offer them social networks to share to, or try out the new Web Share API to integrate with the native sharing system on Android.

## Site is responsive across phone, tablet and desktop screen sizes
To Test	View the PWA on small, medium and large screens and ensure it works reasonably on all.
To Fix	Review our guide on implementing responsive UIs.

## Any app install prompts are not used excessively
To Test	Check the PWA doesn't use an app install interstitial when loaded
To Fix	
There should only be one top or bottom app install banner
After the PWA is added to the user's home screen, any top/bottom banners should be removed.

## The Add to Home Screen prompt is intercepted
To Test	Check the browser doesn't display the A2HS at an inopportune moment, such as when the user is in the middle of a flow that shouldn't be interrupted, or when another prompt is already displayed on the screen.
To Fix	
Intercept the beforeinstallprompt event and prompt later
Chrome manages when to trigger the prompt but for situations this might not be ideal. You can defer the prompt to a later time in the app's usage. It may also help to dim the screen, as advised for requesting permissions below.


# Performance

## First load very fast even on 3G
To Test	Use Lighthouse on a Nexus 5 (or similar) to verify time to interactive <5s for first visit on a simulated 3G network (as opposed to the 10s goal for baseline PWAs)
To Fix	
* Review the performance section of WebFundamentals and ensure you're following the best practices.
* You can understand your performance better by using Pagespeed Insights (aim for a score >85) and SpeedIndex on WebPageTest (aim for a score <4000 on the first view on Mobile 3G Nexus 5 Chrome).
* A few tips are to focus on loading less script, make sure as much script is loaded asynchronously as possible using <script async> and make sure render blocking CSS is marked as such.

# Caching

## Site uses cache-first networking
To Test	
Set the network emulation to the slowest setting and browse around the app.
Then, set the network emulation to offline and browse around. The app should not feel faster when offline than on a slow connection.
To Fix	Use cache-first responses wherever possible. Also review our set of service worker libraries that make implementing these kinds of patterns easier.
## Site appropriately informs the user when they're offline
To Test	Emulate an offline network and verify the PWA provides an indication that you are offline.
To Fix	Use the Network Information API to show the user an indication when they're offline.


# Push notifications

This check list only applies if notifications are implemented. Adding push notifications is not a requirement for an exemplary progressive web app.

## Provide context to the user about how notifications will be used
To Test	
* Visit the site, and find the push notifications opt-in flow
* When you are shown the permission request by the browser, ensure that context has been provided explaining what the site wants the permission for.
* If the site is requesting for the permission on page load, ensure it provides very clear context simultaneously for why the user should enable push notifications.
To Fix	See our guide to creating user-friendly Notifications permissions flows.

## Provide context to the user about how notifications will be used.
To Test	Visit the site and find the push notifications opt in flow. Ensure that if you dismiss or decline to turn on push notifications that the site does not re-prompt in the same way within the same session.
To Fix	If users say they don't want a certain kind of notification, do not reprompt for at least a few days (for example, one week).

## Site dims the screen when permission request is showing
To Test	Visit the site and find the push notifications opt-in flow. When Chrome is showing the permission request, ensure that the page is "dimming" (placing a dark overlay over) all content not relevant to explaining why the site needs push notifications.
To Fix	When calling Notification.requestPermission dim the screen. Undim it when the promise resolves.

## Push notifications must be timely, precise and relevant
To Test:	Enable push notifications from the site and ensure the use cases they're using the push notifications for are:
* Timely — A timely notification is one that appears when users want it and when it matters to them.
* Precise — A precise notification is one that has specific information that can be acted on immediately.
* Relevant — A relevant message is one about people or subjects that the user cares about.
To Fix:	See our guide on creating great push notifications for advice. If your content is not timely and relevant to this user, consider using email instead.

## Provides controls to enable and disable notifications
To Test:	Enable push notifications from the site. Ensure there is some place on the site that allows you to manage your notifications permissions or disable them.
To Fix:	Create a UI that allows users to manage their notification preferences.


# Additional features

## User is logged in across devices via Credential Management API
This only applies if your site has a sign in flow.
To Test:	
* Create an account for a service and ensure you see the save password/account dialog show up. Click "Save".
* Clear cookies for the site (via clicking on the padlock or Chrome settings) and refresh the site. Ensure that you either see an account picker (e.g. if there are multiple accounts saved) or are automatically signed back in.
* Sign out and refresh the site. Ensure that you see the account picker.
To Fix:	Follow our Credential Management API Integration Guide

## User can pay easily via native UI from Payment Request API.

This check only applies if your site accepts payments.
To Test:	Enter the payment flow. Instead of filling out a conventional form, verify the user is able to pay easily via the native UI triggered by the Payment Request API.
To Fix:	Follow our Payment Request API Integration Guide.
