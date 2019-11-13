### Use .env for config

Use dot files to config all the api keys, URLS/domains and etc

Create a .env file in your app's root folder and make sure to not checkin the file to git repo

Dotenv is commonly used (create-react-app uses it) and will get the variables from our .env file and add them to the global process.env.

`vim /my-app-directory/.env`

```bash
API_BASE_URL=http://prod.crio.do
FIREBASE_URL=https://crio-do-dev.appspot.com
FIREBASE_DB_URL=https://crio-do-dev.firebaseio.com
GCLOUD_STORAGE_BUCKET=crio-do-dev.appspot.com
FIREBASE_API_KEY=AIzaSyCxuahB0__3caabIoT543lYf_PI2r0D980
FIREBASE_AUTH_DOMAIN=crio-do-dev.firebaseapp.com
CDN_URL=https://akamai.crio.do
```

Then, you can use the below code to access this URL constant wherever you need

```js
process.env.API_BASE_URL
```

For eg: you might want to use it in your axios instance file
File `/src/utils/axios-helper.js`

```js
const instance = axios.create({
  baseURL: process.env.API_BASE_URL,
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});
```
So, if you want to change the base url in the future, all you have to do is go to the .env file and update the URL and it get's used everywhere else

### Using .env for different environments - `development`, `production` or `test`

create a file in your app's root directory with the relevant environment name like shown below

`vim /my-app-directory/.env.production` and store all the production keys, urls in it

Similarly,

`vim /my-app-directory/.env.development` for storing dev keys, urls and constants

`vim /my-app-directory/.env.test` for storing test keys, urls and constants

When you run 

`npm start` it takes the .env.development configs

`npm test` it takes the .env.test configs

`npm build` will take the .env.production configs
