# Progressive Web Apps
Progressive web apps could be the next big thing for the mobile web.
Originally proposed by Google in 2015, they have already attracted a lot of attention because of the relative ease of development
and the almost instant wins for the application’s user experience.

A progressive web application takes advantage of the latest technologies to combine the best of web and mobile apps.
Think of it as a website built using web technologies but that acts and feels like an app.
Recent advancements in the browser and in the availability of service workers and in the Cache and Push APIs have enabled web developers
to allow users to install web apps to their home screen, receive push notifications and even work offline.

Progressive web apps take advantage of the much larger web ecosystem, plugins and community and the relative ease of deploying
and maintaining a website when compared to a native application in the respective app stores. For those of you who develop
on both mobile and web, you’ll appreciate that a website can be built in less time, that an API does not need to be maintained
with backwards-compatibility (all users will run the same version of your website’s code, unlike the version fragmentation 
of native apps) and that the app will generally be easier to deploy and maintain.

# Why Progressive Web Apps?

A study has shown that, on average, an app loses 20% of its users for every step between the user’s first contact with the app
and the user starting to use the app. A user must first find the app in an app store, download it, install it and then, finally, open it.
When a user finds your progressive web app, they will be able to immediately start using it, 
eliminating the unnecessary downloading and installation stages. And when the user returns to the app,
they will be prompted to install the app and upgrade to a full-screen experience.

However, a native app is definitely not all bad. Mobile applications with push notifications achieve up to three times more retention
than their counterparts without push, and a user is three times more likely to reopen a mobile application than a website. In addition, 
a well-designed mobile application consumes less data and is much faster because some resources reside on the device.

A progressive web application takes advantage of a mobile app’s characteristics, resulting in improved user retention and performance,
without the complications involved in maintaining a mobile application.

# Characteristics Of A Progressive Web App

Before we jump into the code, it is important to understand that progressive web apps have the following characteristics:



# Use cases 
When should you build a progressive web app? Native is usually recommended for applications that you expect users to return to frequently,
and a progressive web app is not any different. Flipkart uses a progressive web app for its popular e-commerce platform, 
Flipkart Lite, and Air Berlin uses a progressive web app for its online check-in process, allowing users to access their tickets
 without an Internet connection.

When assessing whether your next application should be a progressive web app, a website or a native mobile application,
first identify your users and the most important user actions. Being “progressive,” a progressive web app works in all browsers,
and the experience is enhanced whenever the user’s browser is updated with new and improved features and APIs.

Thus, there is no compromise in the user experience with a progressive web app compared to a traditional website; however,
you may have to decide what functionality to support offline, and you will have to facilitate navigation (remember that in standalone mode,
the user does not have access to the back button). If your website already has an application-like interface,
applying the concepts of progressive web apps will only make it better.

If certain features are required for critical user actions but are not yet available due to a lack of cross-browser support,
then a native mobile application might be the better option, guaranteeing the same experience for all users.

# Characteristics Of A Progressive Web App Link

Before we jump into the code, it is important to understand that progressive web apps have the following characteristics:

## Progressive

By definition, a progressive web app must work on any device and enhance progressively, taking advantage of any features available on the user’s device and browser.

## Discoverable

Because a progressive web app is a website, it should be discoverable in search engines. This is a major advantage over native applications, which still lag behind websites in searchability.

## Linkable

As another characteristic inherited from websites, a well-designed website should use the URI to indicate the current state of the application. This will enable the web app to retain or reload its state when the user bookmarks or shares the app’s URL.

## Responsive

A progressive web app’s UI must fit the device’s form factor and screen size.

## App-like

A progressive web app should look like a native app and be built on the application shell model, with minimal page refreshes.

## Connectivity-independent

It should work in areas of low connectivity or offline (our favorite characteristic).

## Re-engageable

Mobile app users are more likely to reuse their apps, and progressive web apps are intended to achieve the same goals through features such as push notifications.

## Installable

A progressive web app can be installed on the device’s home screen, making it readily available.

## Fresh

When new content is published and the user is connected to the Internet, that content should be made available in the app.

## Safe

Because a progressive web app has a more intimate user experience and because all network requests can be intercepted through service workers, it is imperative that the app be hosted over HTTPS to prevent man-in-the-middle attacks.

# Web App manifest

Let’s make our web app more app-like. A web app manifest file is a simple JSON file that follows the W3C’s specification.
With it, it is possible to run the web app in full-screen mode as a standalone application,
to assign an icon that will get displayed when the application is installed on the device,
and to assign a theme and background color to the app. 
In addition, Chrome on Android will proactively suggest that the user install the web app,
via a web app install banner.

To display the installation prompt, your web app needs to:

    1. have a valid web app manifest file,
    2. be served over HTTPS,
    3. have a valid service worker registered,
    4. have been visited twice, with at least five minutes between each visit.

## Manifest JSON
```html
{
    "short_name": "Arrivals",
    "name": "Arrivals at Sky High",
    "description": "Progressive web application demonstration",
    "icons": [
        {
            "src": "launcher-icon.png",
            "sizes": "48x48",
            "type": "image/png"
        },
        {
            "src": "launcher-icon-96.png",
            "sizes": "96x96",
            "type": "image/png"
        },
        {
            "src": "launcher-icon-144.png",
            "sizes": "144x144",
            "type": "image/png"
        },
        {
            "src": "launcher-icon-192.png",
            "sizes": "192x192",
            "type": "image/png"
        },
        {
            "src": "launcher-icon-256.png",
            "sizes": "256x256",
            "type": "image/png"
        }
    ],
    "start_url": "./?utm_source=web_app_manifest",
    "display": "standalone",
    "orientation": "portrait",
    "theme_color": "#29BDBB",
    "background_color": "#29BDBB"
}
```

Let’s break down this manifest file:

* **short_name** is a human-readable name for the application. In Chrome for Android, this is also the name accompanying the icon on the home screen.
* **name** is also a human-readable name for the application and defines how the application will be listed.
* **description** provides a general description of the web application.
* **icons** defines an array of images of varying sizes that will serve as the application’s icon set. In Chrome for Android, the icon will be used on the splash screen, on the home screen and in the task switcher.
* **start_url** is the starting URL of the application.
* **display** defines the default display mode for the web application: fullscreen, standalone, minimal-ui or browser.
* **orientation** defines the default orientation for the web application: portrait or landscape.
* **theme_color** is the default theme color for the application. On Android, this is also used to color the status bar.
* **background_color** defines the background color of the web application. In Chrome, it also defines the background color of the splash screen.
* **related_applications** is not implemented in our example but is used to specify native application alternatives in the various app stores.

Add the manifest.json reference to the index.html file’s head tag:
 ```html
<link rel="manifest" href="./manifest.json">
```
Once a user has added the web app to their home screen, they will be able to re-engage with your application immediately from their device,
without having to directly open the browser. You can see how this is much more than a web bookmark.

# Service Workers

One of the more exciting aspects of progressive web apps is that they can work offline.
Using service workers, it is possible to show data that was retrieved in previous sessions of the app (using IndexedDB) or, alternatively,
to show the application shell and inform the user that they are not connected to the Internet (the approach we’ve taken in this demo).

Once the user reconnects, we can then retrieve the latest data from the server.
All of this is possible through service workers, which are event-driven scripts (written in JavaScript)
that have access to domain-wide events, including network fetches.

With them, we can cache all static resources, which could drastically reduce network requests and improve performance considerably, too.

# Application Shell
The application shell is the minimum HTML, CSS and JavaScript required to power a user interface.
A native mobile application includes the application shell as part of its distributable,
whereas websites ordinarily request this over the network.

App shell architecture separates the core application infrastructure and UI from the data.
All of the UI and infrastructure is cached locally using a service worker so that on subsequent loads,
the Progressive Web App only needs to retrieve the necessary data, instead of having to load everything.

Put another way, the app shell is similar to the bundle of code that you'd publish to an app store when building a native app.
It is the core components necessary to get your app off the ground, but likely does not contain the data.

# Why use the App Shell architecture?

Using the app shell architecture allows you to focus on speed, giving your Progressive Web App similar properties to native apps:
instant loading and regular updates, all without the need of an app store.

To get started with service workers, we first need to create our service worker’s JavaScript file, sw.js, **placed in the root directory**.

# Use service workers to pre-cache the App Shell

Progressive Web Apps have to be fast, and installable, which means that they work online, offline, and on intermittent, slow connections.
To achieve this, we need to cache our app shell using service worker, so that it's always available quickly and reliably.

# SW.JS

 ```html

 // Use a cacheName for cache versioning
        var cacheName = 'v1:static';

// During the installation phase, you'll usually want to cache static assets.
        self.addEventListener('install', function(e) {
            // Once the service worker is installed, go ahead and fetch the resources to make this work offline.
            e.waitUntil(
                caches.open(cacheName).then(function(cache) {
                    return cache.addAll([
                        './',
                        './css/style.css',
                        './js/build/script.min.js',
                        './js/build/vendor.min.js',
                        './css/fonts/roboto.woff',
                        './offline.html'
                    ]).then(function() {
                        self.skipWaiting();
                    });
                })
            );
        });

// when the browser fetches a URL…
        self.addEventListener('fetch', function(event) {
            // … either respond with the cached object or go ahead and fetch the actual URL
            event.respondWith(
                caches.match(event.request).then(function(response) {
                    if (response) {
                        // retrieve from cache
                        return response;
                    }
                    // fetch as normal
                    return fetch(event.request);
                })
            );
        });
```

Let’s look more closely at our service worker. First, we are setting a cacheName variable.
This is used to determine whether any changes have been made to our cached assets.
For this example, we will be using a static name, meaning that our assets will not change or require updating.
```html
        self.addEventListener('install', function(e) {
            // declare which assets to cache
        }
```

The install event fires during the installation phase of the service worker and will fire only once if the service worker is already installed.
Therefore, refreshing the page will not trigger the installation phase again. During the installation phase,
we are able to declare which assets will be cached. In our example above, we are caching one CSS file,
two JavaScript files, our fonts file, our offline HTML template and, of course, the application root. self.skipWaiting() 
forces the waiting service worker to become active.
So far, we have declared our service worker, but before we see it kick into effect, we need to reference it in our JavaScript.
In our application, we register it in main.js

```
            // Register the service worker if available.
            if ('serviceWorker' in navigator) {
                navigator.serviceWorker.register('./sw.js').then(function(reg) {
                    console.log('Successfully registered service worker', reg);
                }).catch(function(err) {
                    console.warn('Error whilst registering service worker', err);
                });
            }

            window.addEventListener('online', function(e) {
                // Resync data with server.
                console.log("You are online");
                Page.hideOfflineWarning();
                Arrivals.loadData();
            }, false);

            window.addEventListener('offline', function(e) {
                // Queue up events for server.
                console.log("You are offline");
                Page.showOfflineWarning();
            }, false);

            // Check if the user is connected.
            if (navigator.onLine) {
                Arrivals.loadData();
            } else {
                // Show offline message
                Page.showOfflineWarning();
            }

            // Set Knockout view model bindings.
            ko.applyBindings(Page.vm);
```

We’ve also included two event listeners to check whether the session’s state has changed from online to offline or vice versa.
The event handlers then call the different functions to retrieve the data through Arrivals.loadData() and to enable
or disable the offline message through Page.showOfflineWarning and Page.hideOfflineWarning, respectively.

Our application also checks whether the user is currently online, using navigator.onLine, and either retrieves the data 
or shows the offline warning accordingly. And in the last line of main.js, we apply the Knockout bindings to our View Model Page.vm.
If we load our application for the first time (with Chrome Developer Tools), we will see nothing new.
However, upon reloading, we will see that a number of network resource have been retrieved from the service worker.

This is our application shell. (img)


******************************************************************************************************************

If you’ve been following the web development community these last few months, chances are you’ve read about progressive web apps (PWAs).
It’s an umbrella term used to describe web experiences so advanced that they compete with ever-so-rich and immersive native apps:
    * full offline support 
    * installability
    * “Retina,”
    * full-bleed imagery
    * sign-in support for personalization
    * faster
    * smooth in-app browsing
    * push notifications 
    * great UI

But even though the new Service Worker API allows you to cache away all of your website’s assets for an almost instant subsequent load,
like when meeting someone new, the first impression is what counts. If the first load takes more than 3 seconds,
the latest DoubleClick study shows that more than 53% of all users will drop off.

And 3 seconds, let’s be real, is already a quite brutal target.
On mobile connections, which often average around a 300-millisecond latency and come with other constraints such as limited bandwidth
and a sometimes poor signal connection, you might be left with a total load performance budget of less than 1 second to actually do the things you need to do to initialize your app.