# Déroulé
Présentation
Tour de table
Le but c'est pas de bêtement suivre des slides, moi mon but c'est que je comprenniez mes explication, ne jamais hésiter a m'interrompre si vous comprennez pas un truc je suis la pour ça
Si il faut reexpliquer, je reexplique
# MVC
- **GET** tous les utilisateurs : `GET http://localhost:3000/api/users`
	- curl -X GET http://localhost:3001/api/users
- **GET** un utilisateur par ID : `GET http://localhost:3000/api/users/1`
	- curl -X GET http://localhost:3001/api/users/1
- **POST** un nouvel utilisateur : `POST http://localhost:3000/api/users` avec le corps JSON `{"name": "John Doe", "email": "john@example.com"}`
	- curl -X POST http://localhost:3001/api/users \
-H "Content-Type: application/json" \
-d '{"name": "John Doe", "email": "john@example.com"}'
- **PUT** mettre à jour un utilisateur : `PUT http://localhost:3000/api/users/1` avec le corps JSON `{"name": "Jane Doe", "email": "jane@example.com"}`
	- curl -X PUT http://localhost:3001/api/users/1 \
-H "Content-Type: application/json" \
-d '{"name": "Jane Doe", "email": "jane@example.com"}'

- **DELETE** un utilisateur : `DELETE http://localhost:3000/api/users/1`
	- curl -X DELETE http://localhost:3001/api/users/1
# Call API Météo

```curl https://api.open-meteo.com/v1/forecast?latitude=52.52&longitude=13.41&current=temperature_2m,wind_speed_10m&hourly=temperature_2m,relative_humidity_2m,wind_speed_10m```

# Login API

Login / get token
`curl -X POST http://localhost:3000/login -H "Content-Type: application/json" -d '{"email":"user@example.com", "password":"userpassword"}'`

Get info with token
`curl -X GET http://localhost:3000/account -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsImlhdCI6MTczMDgxOTQzOSwiZXhwIjoxNzMwODIzMDM5fQ.t9uCkavP4VBxempPTrvP5jV61R4GB3E4EekhYE7zcrk"`

# sec
```
app.use((req, res, next) => { res.removeHeader("X-Powered-By"); // Supprime l'en-tête "X-Powered-By" next(); });
```

# OAUTH
```
const passport = require('passport');
const OAuth2Strategy = require('passport-oauth2');

// Configuration de Passport avec OAuth2
passport.use(new OAuth2Strategy({
    authorizationURL: 'https://provider.com/oauth2/authorize',
    tokenURL: 'https://provider.com/oauth2/token',
    clientID: 'CLIENT_ID',
    clientSecret: 'CLIENT_SECRET',
    callbackURL: 'https://example.com/auth/provider/callback'
  },
  (accessToken, refreshToken, profile, cb) => {
    // Logique pour trouver ou créer l'utilisateur
    User.findOrCreate({ providerId: profile.id }, (err, user) => {
      return cb(err, user);
    });
  }
));

// Endpoint pour déclencher l'authentification
app.get('/auth/provider', passport.authenticate('oauth2'));

// Endpoint de callback après authentification
app.get('/auth/provider/callback', 
  passport.authenticate('oauth2', { failureRedirect: '/login' }),
  (req, res) => {
    res.redirect('/');
  });
```

# JWT

```
const jwt = require('jsonwebtoken');

const user = { id: 1, username: 'user' };
const secretKey = 'votre_clé_secrète';

const token = jwt.sign(user, secretKey, { expiresIn: '1h' });
console.log('Token généré :', token);

```

