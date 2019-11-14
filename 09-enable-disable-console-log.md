### Enable and disable console.log using a single switch

To do that, we can wrap our console.log in a wrapper function which can be customized according to our requirements

Create file `/src/utils/logger.js`

```js
const enableLog = false;
const log = (...msgs) => {
  if (process.env.NODE_ENV === "development" || enableLog) console.log(...msgs);
};

export default log;

```

In the above file, we can set `enableLog = true` if you want to log messages in production. Otherwise, by default this will only log in development environment.

Then, in your component or actions or other js files just do the following

File `/src/actions/homeAction.js`

```js
import log from "../utils/log"

log("homeAction", "Triggered the action call")
```
