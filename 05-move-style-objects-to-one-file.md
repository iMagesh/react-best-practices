### Move style objects to one common file
  To avoid duplicating the same styles again and again
  
File `/src/utils/style-helper.js`

```js
export const menuStyles = {
  baseStyle: {
      height: "fit-content",
      minWidth: "40px",
      width: "fit-content",
      color: "#fff",
    },
  skillTile: {
      ...style.baseStyle,
      fontFamily: theme.typography.primary.main,
      fontSize: "14px",
      fontWeight: "500",
      lineHeight: "16px",
      backgroundColor: "#8899FF",
      padding: "2px 15px",
      borderRadius: "4px",
      margin: "6px",
      textAlign: "center"
    },
    skillContainer: {
      ...style.baseStyle,
      marginTop: "10px",
      display: "flex",
      flexWrap: "wrap"
    }
}

export const aboutStyles = {
  ...
}
```

Then you can import the style helper inside the respective component like,

File `/src/components/ModuleDetail/MeOverview.js`

```js
import { menuStyles } from "../utils/style-helper.js"

render(){
  return(
    <div className={menuStyles.skillTitle}>
    </div>
    <div className={menuStyles.skillContainer}>
    </div>
  )
}
```
