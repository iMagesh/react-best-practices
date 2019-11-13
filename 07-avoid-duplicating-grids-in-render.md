### Avoid duplicating Grids in render

Create a separate file for Grid container that can be re-used in multiple components

File `/src/components/common/GridContainer.js`

```js
<Grid container style={{ width: "100%" }}>
  <Grid item xs={12} className={classes.moduleHeader}>
    <Grid container>
      <Grid item xs={8}>
        <Typography
          type="subHeader"
          style={{
            fontSize: "24px",
            fontFamily: "Prompt",
            padding: "10px"
          }}
        >
          {this.getMeTitle(this.props.currentMETitle)}
        </Typography>
          {this.props.children} // this allows you to add custom content inside the grid container
      </Grid>
    </Grid>
  </Grid>
</Grid>
```

Now, you can reuse the above Grid container in multiple components that requires it instead of duplicating the above code in muliple places

For eg: we will be using the Grid container in following file

File `/src/containers/ModuleDetail/IntroductionModule.js`

```js
import GridContainer from "../../components/common/GridContainer.js"

class IntroductionModule extends Component {
  ...
  render(){
    <GridContainer currentMETitle={this.props.dashboardData.currentME}>
      {// we can add more custom code here}
      <CustomComponentNeededForThisFile />
    </GridContainer>
  }
}
```
