# POST Method



## Making POST

We can directly tap into express framework and utilize everything in it to create a request of POST method.

```javascript
router.post("/user_create", (req, res) => {
	console.log("In user Create service API endpoint");
	console.log("Logging the req of post data", req.body);
	// console.log(req);
	console.log("Getting params", req.params);
	console.log(req.query.location);

	const name = req.query.name;
	const location = req.query.location;
	const job_type = req.query.job_type;
	const email = req.query.email;
	const phone_no = req.query.phone_no;

	/* Sample Query
	INSERT INTO users (name, location, job_type, email, phone_no)
	VALUES("Test2", "Boston", "lol", "asf@gmail.com", 666666666)
	*/

	const queryString =
		"INSERT INTO users (name, location, job_type, email, phone_no) VALUES (?, ?, ?, ?, ?)";
	const connection = getCustomConnection("aws");
	connection.query(
		queryString,
		[name, location, job_type, email, phone_no],
		(err, results, field) => {
			if (err) {
				console.log("Error in the executing query", err);
				res.sendStatus(500);
				return;
			}
			console.log(
				"Inserted data to Database",
				name,
				location,
				job_type,
				email,
				phone_no,
			);

			// We can't use "res object while in the body of executing the query"
			// res.send('Inserted data to Database', first_name, last_name);
			res.end();
		},
	);

	res.end();
});
```


[Parse Post request.](http://www.kompulsa.com/how-to-accept-and-parse-post-requests-in-node-js/)