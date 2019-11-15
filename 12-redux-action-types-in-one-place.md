### Redux action types strings should be saved to a constant in one place

File `/src/actions/action_types.js`

```js
// login actions types
export const SET_LOGIN_DATA = "SET_LOGIN_DATA";
export const UNSET_LOGIN_DATA = "UNSET_LOGIN_DATA";
export const SET_USER_PROFILE_DATA = "SET_USER_PROFILE_DATA";

//home action types
export const ADD_ME_LIST = "ADD_ME_LIST";
export const ADD_MODULE_LIST = "ADD_MODULE_LIST";
export const HIDE_MODAL = "HIDE_MODAL";
```

Then it can be imported wherever required like,

File `/src/actions/loginAction.js`

```js
import {
  SET_LOGIN_DATA,
  UNSET_LOGIN_DATA,
  SET_USER_PROFILE_DATA
} from "./types";

function loginAction = () => {
  return {type: SET_LOGIN_DATA, payload: {}}
}
...
```
