# Section 2

## 5. HTTP & the Node HTTP Module

-   We learn about the `http` module (built into Node.js)
-   See (https://nodejs.org/api/http.html) and (https://www.w3schools.com/nodejs/nodejs_http.asp)
-   We are concerned about the `createServer` method:

```js
// 1. get the http module (comes with Node.js)
const http = require("http");

// 2. create a server object
const server = http.createServer((req, res) => {
	// =================== do thing with req (request that client sends to server) ===================
	let body = [];
	req
        .on("data", (chunk) => {
	    	body.push(chunk);
	    })
	    // req.on() returns an instance of itself so a subsequent .on() is possible
        .on("end", () => {
	    	body = Buffer.concat(body).toString();
	    	console.log(body);
	    });

	// =================== do thing with res (response that server sends to client) ===================
	// write head of the response
	res.writeHead(200, { "Content-Type": "application/json", "X-Powered-By": "Node.js" }); // content type can be `text/html`, for example

	// .end() sends data back to the client
	res.end(JSON.stringify({ success: true, data: body }));
});

// 3. turn server on on a port
const PORT = 5000;
server.listen(5000, () => {
	console.log(`Server running on PORT ${PORT}`);
});
```

## 6. Installing Nodemon

1. Install nodemon as a dev dependency: `npm i --dev nodemon`
2. Add a nodemon script like so:

```json
	"scripts": {
		"start": "nodemon server.js"
	},
```

3. Type `npm start` in terminal
4. Changes in your file and saving will automatically re-run your server

## 7. HTTP Status Codes

-   1.xx Informational
-   2.xx Success
-   200 Success
-   201 Created
-   204 No Content
-   3.xx Redirection
-   304 Not Modified
-   4.xx Client Error
-   400 Bad Request
-   401 Unauthorized
-   404 Not Found
-   5.xx Server Error
-   500 Internal Server Error

## 8. HTTP Request Methods

1. GET - Retrieve Resource
2. POST - Add a Resource
3. PUT - Update Resource
4. DELETE - Delete Resource
