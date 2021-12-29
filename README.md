# how-to-host-web-and-server-in-heroku

# Hosting in HEROKU

## Before hosting website and server in HEROKU, we need to install it's CLI
<a href="https://devcenter.heroku.com/articles/heroku-cli">Click to download</a>

## step-1:
+ Keep the `client folder` into the `server folder` so that both will be hosted at same domain

## step-2:
+ From `package.json` of client folder remove `"proxy":"http://localhost:5000"`

## step-3:
+ In the server folder, in `app.js` file add following code above `app.listen()` method
```
  if (process.env.NODE_ENV == "production") {
  app.use(express.static("client/build"));
  const path = require("path");
  app.get("*", (res, req) => {
    res.sendFile(path.resolve(__dirname, "client", "build", "index.html"));
  });
}
```

## step-4:
+ Replace the following code in the `package.json` of server folder in the `scripts` by
```
 "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "node app.js",
    "heroku-postbuild": "NPM_CONFIG_PRODUCTION=false npm install --prefix client && npm run build --prefix client"
  },
```

## step-5:
+ After doing the above step, it's time to build the client side. so,
```
>>> cd client
>>> npm run build
```

## step-6:
+ After building the client static page. Come to `server folder`
+ And run following code.

```
$ heroku login
``` 
+ By running above code, a window of login get open. Click on login
+ next run following code,
```
$ git add .
$ git commit -am "make it better"
$ git push heroku master

```

## 🎉🎉🎉 Congratulation! Finally we hosted our web 🎉🎉🎉
