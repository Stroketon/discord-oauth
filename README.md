# discord-oauth
Discord oAuth Wrapper created to make using oAuth as easy as possible.

All you have to do to use it is pass a oAuth2 code into the wrapper.

Example:
```javascript
const express = require('express');
const app = express();
app.use(express.json(), express.urlencoded({ extended: true }));
const DiscordoAuth2 = require('discord-oauth');

const oAuth = new DiscordoAuth2({
  client_secret: "your-client-secret",
  client_id: "your-client-id",
  callback: "https://website.com/callbackurl",
});

app.get('/login', (req, res) => {
  res.redirect('DISCORD-OAUTH-AUTHORIZATION-LINK');
});

app.get('call-back-url', async(req, res) => {
  // get the access_token/refresh_token/etc.
  const data = await oAuth.getToken(req.query.code);
  res.send(data)

  // get the user's info.
  const data2 = await oAuth.getUser(req.query.code);
  res.send(data2)
});

app.listen(3000, () => console.log('Listening to port 3000.'))
```
