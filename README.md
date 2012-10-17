# passport-expresshelper #

Helper for express 2.x in combination with the with the passport authentication module


## dynamicHelper for express 2.x: ##


    var passportexpresshelper = require('passport-expresshelper');
    
    app.configure(function(){
        ...
        app.use(passport.initialize());
        app.use(passport.session());
        ...
        app.dynamicHelpers(passportexpresshelper.dynamicHelpers);
        ...
    });


## Middleware for express routes ##

    var checkAuth = require('passport-expresshelper').ensureAuthenticated;
    
    app.get('/somethingprivate', checkAuth);

If the user is authenticated through passport, the request will continue to the requested page. Otherwise the requested path will be saved to ```req.session.redirect``` and the user will be redirected to ```/login```. If you want to forward the user to a different page, you could add another route like this:

    app.get('/login', function(req, res) {
        res.redirect('/auth');
    });

After the login, the user can be forwarded to the originally requested page using the saved path in ```req.session.redirect```.