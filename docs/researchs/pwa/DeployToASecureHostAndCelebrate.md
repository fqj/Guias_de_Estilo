9. Deploy to a secure host and celebrate

The final step is to deploy our weather app to a server that supports HTTPS. If you don't already have one, the absolute easiest (and free) approach is to use the static content hosting from Firebase. It's super easy to use, serves content over HTTPS and is backed by a global CDN.

Extra credit: minify and inline CSS
There's one more thing that you should consider, minifying the key styles and inlining them directly into index.html. Page Speed Insights recommends serving the above the fold content in the first 15k bytes of the request.

See how small you can get the initial request with everything inlined.

Further Reading: PageSpeed Insight Rules

This step requires you to have Node & NPM installed on your system. If it's not, you can use any other hosting provider that supports HTTPS. We've used Firebase because it automatically redirects users from HTTP to HTTPS. If you use a different provider, be sure they're always redirects to HTTPS.

Deploy to Firebase
If you're new to Firebase, you'll need to create your account and install some tools first.

Create a Firebase account at https://firebase.google.com/console/
Install the Firebase tools via npm: npm install -g firebase-tools
Once your account has been created and you've signed in, you're ready to deploy!

Create a new app at https://firebase.google.com/console/
If you haven't recently signed in to the Firebase tools, update your credentials: firebase login
Initialize your app, and provide the directory (likely work) where your completed app lives: firebase init
Finally, deploy the app to Firebase: firebase deploy
Celebrate. You're done! Your app will be deployed to the domain: https://YOUR-FIREBASE-APP.firebaseapp.com
Further reading: Firebase Hosting Guide

Test it out
Try adding the app to your home screen then disconnect the network and verify the app works offline as expected.
TRY IT

