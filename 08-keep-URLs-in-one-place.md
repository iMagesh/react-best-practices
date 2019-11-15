### Keep all the URLs in one place

You can use the .env file like we discussed in [dot env files](https://github.com/iMagesh/react-best-practices/blob/master/03-use-dot-env-files-to-store-api-key-domains-urls.md)

or create a separate URL config file if you do not want to mix the API keys along with URLs

File `/src/configs/url-config.js`

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

You can also keep all the API paths in one file so if there is any change in the path in the future, it can be easily modified since it is all in one file. 

File `/src/configs/api-paths.js`

```js
export const path = {
  HOME: {
    //APIs related to home module will be in here
    LOGIN: "/api/v1/auth/login",
    SIGNUP: "/api/v1/auth/register",
  }
  ME: {
    //APIs related to ME Modules will go in here
    GET_ALL_MODULES: "/api/v1/ME/modules",
  }
}

```

Then you can update the below file like,

File `/src/actions/loginAction.js`

```js
import { urls } from "../../config/url-config"
import { path } from "../../config/api-paths"

export const doLogin = accessToken => {
  return dispatch => {
    console.log("In Login Action");
    return fetch(urls.API_END_POINT + path.HOME.LOGIN, {
      config
    })
      .then(res => res.json()) // expecting a json response
      .then(json => console.log(json));
  };
};
```

