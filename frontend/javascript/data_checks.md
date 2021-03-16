Data Checks

## Network Response

Checking network response is also good defensive practice but due to Javascript failing so gracefully, web developers tend to overlook this when writing the functions.

```javascript
function networkCall() {
	var request = new XMLHttpRequest();
	var getRescueTime =
		"https://www.rescuetime.com/anapi/daily_summary_feed?key=qagnak";

	// call url
	request.open("GET", getRescueTime);
	request.onreadystatechange = function () {
		if (this.readyState === 4) {
			this.getAllResponseHeaders();
			//Converting responseText String JSON to Javascript Object JSON.
			var rescueTimeJSON = this.responseText;
			
			// Null Check whether the data is present
			if (rescueTimeJSON) {
				var rescueTimeObj = JSON.parse(rescueTimeJSON);
			}
		}
	};
	request.send();
}

```


[SO](https://stackoverflow.com/questions/154059/how-can-i-check-for-an-empty-undefined-null-string-in-javascript)