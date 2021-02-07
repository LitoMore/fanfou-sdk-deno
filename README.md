# fanfou-sdk-deno

Fanfou SDK for Deno

## Install

```javascript
import Fanfou from "https://deno.land/x/fanfou_sdk/index.js";
```

## Usage

**OAuth**

```javascript
const ff = new Fanfou({
  consumerKey: "",
  consumerSecret: "",
  oauthToken: "",
  oauthTokenSecret: "",
});

const timeline = await ff.get("/statuses/home_timeline", { format: "html" });
```

**XAuth**

```javascript
const ff = new Fanfou({
  consumerKey: "",
  consumerSecret: "",
  username: "",
  password: "",
});

await ff.xauth();

const timeline = await ff.get("/statuses/public_timeline", { count: 10 });
const status = await ff.post("/statuses/update", { status: "Hi Fanfou" });
```

**Options**

- `consumerKey`: The consumer key
- `consumerSecret`: The consumer secret
- `oauthToken`: The OAuth token
- `oauthTokenSecret`: The OAuth token secret
- `username`: The Fanfou username
- `password`: The Fanfou password
- `protocol`: Set the prototol, default is `http:`
- `apiDomain`: Set the API domain, default is `api.fanfou.com`
- `oauthDomain`: Set the OAuth domain, default is `fanfou.com`
- `hooks`: Hooks allow modifications with OAuth

> For more Fanfou API docs, see the
> [Fanfou API doc](https://github.com/FanfouAPI/FanFouAPIDoc/wiki).

## API

```javascript
ff.getRequestToken();
ff.getAccessToken(token);
ff.xauth();
ff.get(uri, params);
ff.post(uri, params);
ff.upload(uri, params);
```

**Examples**

```javascript
// Get request token
const token = await ff.getRequestToken();

// Get access token
const token = await ff.getAccessToken(token);

// Get timeline
const timeline = await ff.get("/statuses/home_timeline", {});

// Post status
const status = await ff.post("/statuses/update", { status: "post test" });

// Upload photo
const result = await ff.upload("/photos/upload", {
  photo: uploadFile,
  status: "unicorn",
});
```

**Tips**

Use `hooks` for your reverse-proxy server

```javascript
const ff = new Fanfou({
  consumerKey: "",
  consumerSecret: "",
  oauthToken: "",
  oauthTokenSecret: "",
  apiDomain: "api.example.com",
  oauthDomain: "example.com",
  hooks: {
    baseString: (str) => {
      return str.replace("example.com", "fanfou.com");
    },
  },
});
```

## Related

- [fanfou-sdk-node](https://github.com/fanfoujs/fanfou-sdk-node) - Fanfou SDK
  for Node.js
- [fanfou-sdk-browser](https://github.com/fanfoujs/fanfou-sdk-browser) - Fanfou
  SDK for browser
- [fanfou-sdk-weapp](https://github.com/fanfoujs/fanfou-sdk-weapp) - Fanfou SDK
  for WeApp
- [fanfou-sdk-python](https://github.com/LitoMore/fanfou-sdk-python) - Fanfou
  SDK for Python

## License

MIT
