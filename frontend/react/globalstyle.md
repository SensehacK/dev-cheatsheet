# Global Style

React Native Global Style

## Global CSS

Style.js

```javascript
import { StyleSheet } from 'react-native';

export default StyleSheet.create({
  container: {
    flex: 1
  },
  welcome: {
    fontSize: 20
  }
});
```

In any of the files you want to use your style, add the following:

> import styles from './Style'

[SO Link](https://stackoverflow.com/questions/30853178/react-native-global-styles)

