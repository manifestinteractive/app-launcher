# About

Website at http://launch.yourwebsite.com

Introduction:
---

When the user clicks a link starting with http://launch.yourwebsite.com it hits this service which tries to launch our
app using a custom `appname://` protocol. If the user has our app installed, that `appname://` protocol will exist and the link
will open directly to the spot in our app they are trying to go. If they do not have the app installed, but they are
using an iPhone of Android device, they will be taken to the respective store to install our app. If they are not using
a mobile device, they will be taken to our home page to learn more about the app.

NOTE:  Each link option that allows you to access specific content ( search, events, account access, etc ) needs to use
a "slug" version of the name you are trying to link to. The "slug" is pretty straight forward to figure out.  Just make
everything lower case, and convert spaces to dashes. Also, if there are any characters that are not letters or spaces,
remove them.  ( e.g. a search for "Foo Bar" would become http://launch.yourwebsite.com/search/foo-bar &
the product ID "123" would become http://launch.yourwebsite.com/product/123 )

### Example Usage:

__EXAMPLE DIRECT LINKS TO SEARCH:__

* http://launch.yourwebsite.com/search/foo-bar
* http://launch.yourwebsite.com/search/coffee

__EXAMPLE DIRECT LINKS TO EVENTS:__

* http://launch.yourwebsite.com/product/123
* http://launch.yourwebsite.com/product/456

__EXAMPLE DIRECT LINKS TO MANAGE ACCOUNT:__

* http://launch.yourwebsite.com/account/forgot-password
* http://launch.yourwebsite.com/account/reset-password/N0lXnKCdyLUR
* http://launch.yourwebsite.com/account/confirm/TriqG3m344N8

__EXAMPLE DIRECT LINKS TO APP SPECIFIC PAGES:__

* http://launch.yourwebsite.com/landing
* http://launch.yourwebsite.com/login
* http://launch.yourwebsite.com/register
* http://launch.yourwebsite.com/home
* http://launch.yourwebsite.com/terms
* http://launch.yourwebsite.com/privacy


Installation:
---

This project assumes you are using the [Custom URL Scheme](https://github.com/EddyVerbruggen/Custom-URL-scheme) Cordova
Plugin on a mobile application.

This pluging can easily be installed in your project via:

```basg
cordova plugin add cordova-plugin-customurlscheme --variable URL_SCHEME=appname
```

Once you have this plugin installed in your Cordova App, you will need to host this project on a publicly available
server, e.g. http://launch.yourwebsite.com

You will need to update the index.html file's JavaScript variables to your project needs.

Finally, you will need to add a custom function to your mobile app to handle the incoming arguments for
launching your app.  Something like this could be used as a starter ( note you must name the function `handleOpenURL` ):

```js
/**
 * Handle Open URL
 * @param {String} url appname://account/confirm/TriqG3m344N8
 */
function handleOpenURL(url) {
  var params = [];
  var launchUrl = url.replace('appname://', '');

  if(launchUrl) {

    params = launchUrl.split('/');

    if(params.length > 0) {

      var validPages = [
        'search',
        'product',
        'account',
        'landing',
        'login',
        'register',
        'home',
        'terms',
        'privacy'
      ];

      if(validPages.indexOf(params[0]) > -1) {
        // Call function to open app to these pages and pass optional params
      }
    }
  }
}
```
