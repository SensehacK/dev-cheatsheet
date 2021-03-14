Dark Mode



```javascript
	<!-- Dark Mode Script
	 ================================================== -->
		<script src="https://cdn.jsdelivr.net/npm/darkmode-js@1.5.7/lib/darkmode-js.min.js"></script>
		<script>
			const options = {
				bottom: "64px", // default: '32px'
				right: "unset", // default: '32px'
				left: "32px", // default: 'unset'
				time: "0.5s", // default: '0.3s'
				mixColor: "#fff", // default: '#fff'
				backgroundColor: "#fff", // default: '#fff'
				buttonColorDark: "#100f2c", // default: '#100f2c'
				buttonColorLight: "#fff", // default: '#fff'
				saveInCookies: false, // default: true,
				label: "🌓", // default: ''
				autoMatchOsTheme: true, // default: true
			};
			function addDarkmodeWidget() {
				new Darkmode(options).showWidget();
			}
			window.addEventListener("load", addDarkmodeWidget);
		</script>

```

[dark mode js](https://darkmodejs.learn.uno)