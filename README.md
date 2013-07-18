# Passport-Podio

[Passport](https://github.com/jaredhanson/passport) strategy for authenticating
with [Podio](http://podio.com) using the OAuth 2.0 API.

## Install

    $ npm install passport-podio

## Usage

#### Configure Strategy

The Podio authentication strategy authenticates users using a Podio
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

    passport.use(new PodioStrategy({
        clientID: CLIENT_ID,
        clientSecret: CLIENT_SECRET
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ PodioId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authorize()`, specifying the `'Podio'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/podio',
      passport.authorize('podio'));

    app.get('/auth/podio/callback', 
      passport.authorize('podio', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Thanks

  - [Jared Hanson](http://github.com/jaredhanson)

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2013 Michael Pearson <[http://github.com/mjpearson](http://github.com/mjpearson)>