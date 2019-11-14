### React Error Boundary for handling common render errors in one place

Create a error boundary component that can be used to wrap our other complex components that are prone to render error.
Now, whenever something goes wrong in the render of those child components that are wrapped with the ErrorBoundary component,
we can show a common error page with errorInfo that the component caught just now.

Let's create a error boundary component first

File `/src/components/errors/MeErrorBoundary.js`

```js
class MeErrorBoundary extends React.Component {
      state = { error: null, errorInfo: null };

      componentDidCatch(error, errorInfo) {
        this.setState({
          error: error,
          errorInfo: errorInfo
        });
      }

      render() {
        if (this.state.errorInfo) {
          // if there was an error caught then the following code will be rendered 
          // but the child components will not be rendered
          // if we have more than one child, if one of them has an error none of them will be rendered 
          // instead we show the following:
          return (
            <div>
              <h2>Hold on. Looks like one of our pod has an issue. We are fixing it. Can you try after sometime?</h2>
              <details style={{ whiteSpace: "pre-wrap" }}>
                {this.state.error && this.state.error.toString()}
                <br />
                {this.state.errorInfo.componentStack}
              </details>
            </div>
          );
        }

        return this.props.children; // if there was not error, the child components will be rendered
      }
    }
```

Now how to use the above created ErrorBoundary?

Open our existing component that has a lot of complexity in the render function
eg: File `/src/components/ModuleDetail/CodeTasks/CodeTask.js`

wrap the Grid component with the above created error boundary component like,

```js
<MeErrorBoundary>
  <Grid container spacing={0}>
    <Grid item xs={12}>
      <div
        className={classes.slickContainer}
        style={{ padding: "0 20px", background: "#f6f6f6" }}
      >
        <Carousel
          data={milestoneDetails}
          onSlideClick={this.onSlideClick}
          selectedSlide={this.props.moduleDetails.selectedCodeTask}
          type="code"
        />
      </div>
    </Grid>
  </Grid>
 </MeErrorBoundary>
```

In the above code, if the <Grid /> or <Carousel /> components has a render error, our <MeErrorBoundary /> will catch the error
and display the custom message in the format that we have given (we can also use well designed popup and etc)

We can use ErrorBoundary to wrap components that are suspected to have render issues maybe because of the complexity.
We can have multiple ErrorBoundary for different modules so we can show more specific errors. 

Do not use Boundaries to handle errors in things like event handlers or other stand-alone logic. Stick to try…catch for such cases
