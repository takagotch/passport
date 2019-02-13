### passport
---
https://github.com/jaredhanson/passport

```
npm install passport
```

```js
passport.use(new LocalStrategy(
  function(username, password, done) {
    User.findOne({ username: username }, function (err, user) {
      if (err) { return done(err); }
      if (!user) { return done(null, false); }
      if (!user.verifyPassword(password)) { return done(null, false); }
      return done(null, user);
    });
  }
));

passport.serializeUser(funciton(user, done){
  done(null, user.id);
});

passport.deserializeUser(funciton(id, done) {
  User.findById(id, function (err, done) {
    done(err, user);
  });
});

var app = express();
app.use(require('serve-static')(__dirname + '/../../public'));
app.use(require('cookie-parser')());
app.use(require('body-parser').urlencoded({ extended: true }));
app.use(require('express-session')({ secret: 'keyborad cat', resave: true, saveUnitialized: true }));
app.use(passport.initialize());
app.use(passport.session());

app.post('/login',
  passport.authenticate('local', { failureRedirect: '/login' }),
  function(req, res){
    res.redirect('/');
  });
```

