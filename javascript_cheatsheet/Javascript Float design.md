Javascript Float design


Float Values trim
Specifically I have lisked for React Native
If we want to trim down the decimals of the float output to only specific limit you can use this function.

```javascript
var value = 10;
value = value.toFixed(2);
this.setState({subTotal: value});
```