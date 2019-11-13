For Ajax API calls/requests, create an instance file that can be imported wherever ajax calls are to be done instead of importing the default axios property from the library

Let's add the below code to `/src/utils/ajax-helper.js`

```js
const instance = axios.create({
  baseURL: 'https://some-domain.com/api/',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});
```

You can also pass defaults like this

```js
instance.defaults.baseURL = 'https://api.example.com';
instance.defaults.headers.common['Authorization'] = AUTH_TOKEN;
instance.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
```

And then import the axios instance to make ajax calls like this:

for eg: we can add the below code to `/src/actions/api.js`

```js
Import axios from “../../utils/ajax-helper.js”

axios.get(“/users”)
.then(...)
.catch(...)

```
