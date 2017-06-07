# Background sync
An API that extends Service Workers with an onsync event
Background sync is a new web API that lets you defer actions until the user has stable connectivity.
This is useful for ensuring that whatever the user wants to send, is actually sent.

## The problem

The internet is a great place to waste time. Without wasting time on the internet, we wouldn’t know cats dislike flowers, chameleons love bubbles, and "You do What They Told Ya" as sung by "Rage Against the Machine" sounds like the Japanese for, "Break the chicken nugget, daddy".

But sometimes, just sometimes, we’re not looking to waste time. The desired user experience is more like:

Phone out of pocket.
Achieve minor goal.
Phone back in pocket.
Resume life.

Unfortunately this experience is frequently broken by poor connectivity. We’ve all been there. 
You’re staring at a white screen or a spinner, and you know you should just give up and get on with your life, 
but you give it another 10 seconds just in case. After that 10 seconds? Nothing. But why give up now? 
You’ve invested time already, so walking away with nothing would be a waste, so you carry on waiting. 
By this point you want to give up, but you know the second you do so, 
is the second before everything would have loaded if only you’d waited.

Service workers solve the page loading part by letting you serve content from a cache.
But what about when the page needs to send something to the server?

At the moment, if the user hits "send" on a message they have to stare at a spinner until it completes. 
If they try to navigate away or close the tab, we use onbeforeunload to display a message like, “Nope, I need you to stare at this spinner some more. Sorry”.
If the user has no connection we tell the user “Sorry, you must come back later and try again”.

This is rubbish. Background sync lets you do better.

# The solution

The following video shows Emojoy, a simple emoji-only chat demo… thing. It’s a progressive web app. It works offline-first. It uses push messages and notifications, and it uses background sync.

If the user tries to send a message when they have zero connectivity, then, thankfully, the message is sent in the background once they get connectivity.


As of March 2016, Background sync is available in Chrome from version 49 and above. You can see it action by following the steps below:

Open Emojoy.
Go offline (either using airplane-mode).
Type a message.
Go back to your home screen (optionally close the tab/browser).
Go online.
Message sends in the background!
Being able to send in the background like this also yields a perceived performance improvement.
The app doesn’t need to make such a big deal about the message sending, so it can add the message to the output straight away.



# How to request a background sync

In true extensible web style, this is a low level feature that gives you the freedom to do what you need. 
You ask for an event to be fired when the user has connectivity, which is immediate if the user already has connectivity.
Then, you listen for that event and do whatever you need to do.

Like push messaging, it uses a service worker as the event target, which enables it to work when the page isn’t open.
To begin, register for a sync from a page:
```
        // Register your service worker:
        navigator.serviceWorker.register('/sw.js');

        // Then later, request a one-off sync:
        navigator.serviceWorker.ready.then(function(swRegistration) {
        return swRegistration.sync.register('myFirstSync');
        });
        Then listen for the event in /sw.js:

        self.addEventListener('sync', function(event) {
        if (event.tag == 'myFirstSync') {
            event.waitUntil(doSomeStuff());
        }
        });
```
And that's it! In the above, doSomeStuff() should return a promise indicating the success/failure of whatever it’s trying to do. 
If it fulfills, the sync is complete. If it fails, another sync will be scheduled to retry. 
Retry syncs also wait for connectivity, and employ an exponential back-off.

The tag name of the sync ('myFirstSync' in the above example) should be unique for a given sync.
If you register for a sync using the same tag as a pending sync, it coalesces with the existing sync. 
That means you can register for an "clear-outbox" sync every time the user sends a message, but if they send 5 messages while offline,
you'll only get one sync when they become online. If you want 5 separate sync events, just use unique tags!

Here’s a simple demo that does the bare minimum; it uses the sync event to show a notification.

# What could I use background sync for?

Ideally, you’d use it to schedule any data sending that you care about beyond the life of the page. 
Chat messages, emails, document updates, settings changes, photo uploads… 
anything that you want to reach the server even if user navigates away or closes the tab. 
The page could store these in an "outbox" store in indexedDB, and the service worker would retrieve them, and send them.

Although, you could also use it to fetch small bits of data…

# Permissions

Background sync itself does not require permission.

Sync events will often complete while the user has a page open to the site, so requiring user permission would be a poor experience. 
Instead, we’re limiting when syncs can be registered and triggered to prevent abuse. E.g.:

 * You can only register for a sync event when the user has a window open to the site.
 * The event execution time is capped, so you can’t use them to ping a server every x seconds, mine bitcoins or whatever.
 * Of course, these restrictions may loosen/tighten based on real-world usage.


# Documents 

[https://github.com/WICG/BackgroundSync/blob/master/explainer.md] (Background synchronization explained)
[https://github.com/WICG/BackgroundSync] (WICG/BackgroundSync)