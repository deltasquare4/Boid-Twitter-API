Boid Twitter API
================

This library is still a work in progress, when it's at production level it'll be implemented in Boid for Twitter (http://www.boidapp.com). Feel free to use this library in your own applications when it reaches a completely usable point.

First Time Authentication
----------------

```java
Authorizer auth = Authorizer.create(
                "5LvP1d0cOmkQleJlbKICtg", //Consumer key
                "j44kDQMIDuZZEvvCHy046HSurt8avLuGeip2QnOpHKI",  //Consumer secret
                "myapp://callback");  //Callback URL
        String url = auth.getUrl();
        /**
         * This URL should now be opened in the web browser, it will show Twitter's authentication page
         * where the user logs in and clicks "Authorize." The web browser will then redirect to your
         * callback URL. Your app should intercept this callback.
         */

        // 'oauth_verifier' should be replaced with the 'oauth_verifier' query parameter sent through
        // the callback from the web browser. You now are logged in.
        Twitter twitter = auth.finish("oauth_verifier");

        //These values should be saved to local storage, on Android they can be saved using SharedPreferences.
        //These values can be used later to login without going to the authorization page again.
        String accessToken = twitter.getAccessToken();
        String accessSecret = twitter.getAccessSecret();
```

Logging in with the Access Token and Secret
-----------------

Once you've saved the access token and secret strings shown in the end of the code block above, you can login later without going to the authentication page again (like the commented text says above).

```java
Authorizer auth = Authorizer.create(
                "5LvP1d0cOmkQleJlbKICtg", //Consumer key
                "j44kDQMIDuZZEvvCHy046HSurt8avLuGeip2QnOpHKI",  //Consumer secret
                "myapp://callback");  //Callback URL
        Twitter twitter = auth.getAuthorizedInstance(
                accessToken,  //Insert your access token
                accessSecret);  //Insert your access secret
```

You are now authenticated again for the account you added in the first section.