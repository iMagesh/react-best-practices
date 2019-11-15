### Exporting all the components in one place (index.js)

Create a new file `index.js` inside `/src/components` directory where you can export all the components in one place like,

File `/src/components/index.js`

```js
export { default as App } from "./App";
export { default as Home } from "./Home/HomeIndex";
export { default as Login } from "./Login/Login";
export { default as CodeBody } from "./ModuleDetail/CodeTask/CodeBody.js";
export { default as CodeHeader } from "./ModuleDetail/CodeTask/CodeHeader.js";
export { default as NotFound } from "./common/NotFound";
export { default as Signup } from "./common/Signup";

```

Then in other componets when you have to import a whole bunch of those files it because easier.

File `/src/components/ModuleDetails/CodeTask/Something.js`

```js
import React from "react"
import { Home, CodeHeader, CodeBody, Signup} from "../../index"

...
```

The same can be done for other folders, `containers`, `actions`, `reducers` and so on

