### Avoid duplicating mapStateToProps and mapDispatchToProps in multiple files

Create a helper file for reused redux stateToProps and DispatchToProps functions

File `/src/utils/redux-helpers/common-state-to-props.js`

```js
export const moduleDetailsProps = state => ({
  location: state.location,
  user: state.loginReducer,
  dashboardData: state.MeDashboardReducer
});
```

Then,

Inside your container file, import and pass the function to connect()

File `/src/containers/ModuleDetail/ModuleDetail.js`

```js
import {moduleDetailsProps as mapStateToProps} from "../utils/redux-helpers/common-state-to-props.js"

class ModuleDetail extends Component {
  ...
  ...
}
export default connect(
  mapStateToProps,
  mapDispatchToProps
)(withStyles(styles)(ModuleDetail));

```

The same mapStateToProps is used in another file as well,

File `/src/containers/ModuleDetail/IntroductionModule.js`

```js
import {moduleDetailsProps as mapStateToProps} from "../utils/redux-helpers/common-state-to-props.js"

class IntroductionModule extends Component {
  ...
  ...
}

export default connect(
  mapStateToProps,
  mapDispatchToProps
)(withStyles(styles)(IntroductionModule));

```

Same approach will work for mapDispatchToProps function that are repeated in multiple redux container/components
