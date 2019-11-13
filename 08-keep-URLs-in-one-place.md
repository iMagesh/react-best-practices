### Keep all the URLs in one place

You can use the .env file like we discussed in [dot env files](https://github.com/iMagesh/react-best-practices/blob/master/03-use-dot-env-files-to-store-api-key-domains-urls.md)

or create a separate URL config file if you do not want to mix the API keys along with URLs

File `/configs/url-config.js`

```js
export const urls = {
  CDN_BASE_URL: "https://akamai.crio.do",
  FIREBASE_AUTH_DOMAIN: "http://crio-do-dev.firebaseapp.com",
  GCLOUD_STORAGE_BUCKET: "http://crio-do-dev.appspot.com",
  API_END_POINT: "http://crio-do-dev.appspot.com"
}
```

Then, use it inside your actions like,

File `/src/actions/loginAction.js`

```js
import { urls } from "../../config/url-config"

export const doLogin = accessToken => {
  return dispatch => {
    console.log("In Login Action");
    return fetch(urls.API_END_POINT + "api/v1/auth/login", {
      config
    })
      .then(res => res.json()) // expecting a json response
      .then(json => console.log(json));
  };
};
```
