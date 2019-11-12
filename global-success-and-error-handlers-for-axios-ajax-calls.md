### Create a flag to enable or disable the global handler for success/error response

```js
const isHandlerEnabled = (config={}) => {
  return config.hasOwnProperty('handlerEnabled') && !config.handlerEnabled ? 
    false : true
}
```

we can disable handler for an individual HTTP call if we want to like, 

```js
axiosInstance.get('/v2/api-endpoint', { handlerEnabled: false })
```

### Axios request interceptor

Let's add request handler. You can also intercept request and add headers before the request is sent to server like,

```js
const requestHandler = (request) => {
  if (isHandlerEnabled(request)) {
    // Modify request here
    request.headers['X-CodePen'] = 'https://codepen.io/teroauralinna/full/vPvKWe'
  }
  return request
}
```

Enable request interceptor to make the above code work like,

```js
axiosInstance.interceptors.request.use(
  request => requestHandler(request)
)
```

Now coming back to handling success and error in a global centralized place.

### Using axios response and error interceptors

```js
const errorHandler = (error) => {
  if (isHandlerEnabled(error.config)) {
    // Handle errors
  }
  return Promise.reject({ ...error })
}

const successHandler = (response) => {
  if (isHandlerEnabled(response.config)) {
    // Handle responses
  }
  return response
}
```

### Now Enable interceptors

```js
axiosInstance.interceptors.response.use(
  response => successHandler(response),
  error => errorHandler(error)
)
```
