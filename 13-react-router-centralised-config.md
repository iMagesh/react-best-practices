### React router centralized config

We can have a centralized route config which is just an array of data containing the path, component to be rendered and so on.
The array is ordered in the same way you do inside a `<Switch>`

File /src/routes/all_routes.js

```js
import { ModuleComponent, ModuleOverview } from "../components"
const routes = [
  {
    path: "/",
    component: Home
  },
  {
    path: "/me",
    component: MEComponent,
    routes: [
      {
        path: "/me/:id",
        component: ModuleComponent
      },
      {
        path: "/me/overview",
        component: ModuleOverview
      }
    ]
  }
];

export default routes;

```

File `/src/routes/AppRouter.js`

```js

import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link
} from "react-router-dom";

function RouteWithSubRoutes(route) {
  return (
    <Route
      path={route.path}
      render={props => (
        // pass the sub-routes down to keep nesting
        <route.component {...props} routes={route.routes} />
      )}
    />
  );
}

function AppRouter(){
  return(
    <Router>
      <ul>
        <li>
          <Link to="/me/:moduleId">{props.moduleId}</Link>
        </li>
        <li>
          <Link to="/me/taskBoard">Task board</Link>
        </li>
      </ul>
      
      <Switch>
        {routes.map((route, i) => (
          <RouteWithSubRoutes key={i} {...route} />
        ))}
      </Switch>
    </Router>
  )
}
export default AppRouter;

```

Then,

File `/src/components/Home.js`

```js
import routes from "../routes/all_routes.js"
import AppRouter from "../routes/AppRouter.js"

function Home(props) {
  return (
    <div>
      <h2>Home</h2>
      <AppRouter />
    </div>
  );
}

```
