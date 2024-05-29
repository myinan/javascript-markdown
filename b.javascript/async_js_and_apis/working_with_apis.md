# Working with APIs
## API
An API, or Application Programming Interface, is a set of rules and tools that allows different software applications to communicate with each other. It serves as a bridge between different software systems, enabling them to exchange information and perform specific tasks seamlessly. APIs play a crucial role in modern software development, fostering interoperability and enabling the creation of more powerful and complex applications by leveraging the capabilities of existing services and libraries.

Here are the key components and concepts associated with APIs:

1. **Definition:**
   An API defines the methods and data formats that applications can use to communicate with each other. It essentially specifies how software components should interact, providing a standardized way for developers to integrate various services and functionalities.

2. **Endpoints:**
   APIs expose specific endpoints, which are unique URLs or URIs (Uniform Resource Identifiers), representing different functionalities or resources. Each endpoint corresponds to a specific operation or data set that the API can perform or provide.

3. **Request and Response:**
   Communication between software components through an API typically involves sending requests and receiving responses. A request is made by one application to a specific API endpoint, and the API processes the request and returns relevant data or performs a specific action. The request and response formats are often defined using common data interchange formats like JSON (JavaScript Object Notation) or XML (eXtensible Markup Language).

4. **HTTP Methods:**
   APIs commonly use HTTP methods such as GET, POST, PUT, and DELETE to perform different actions. For example, a GET request is used to retrieve information, while a POST request is used to submit data.

5. **Authentication and Authorization:**
   APIs often implement security measures to control access to their functionalities. This involves authentication, which verifies the identity of the requesting application or user, and authorization, which determines the level of access granted based on the authenticated identity.

6. **Documentation:**
   Good API design includes comprehensive documentation that explains the available endpoints, the expected request and response formats, authentication requirements, and any other relevant information. This documentation helps developers understand how to use the API effectively.

7. **SDKs (Software Development Kits):**
   To simplify the integration process, APIs may come with SDKs, which are sets of pre-built tools, libraries, and documentation that make it easier for developers to interact with the API in their preferred programming languages.

8. **RESTful APIs:**
   Representational State Transfer (REST) is a common architectural style for designing networked applications. RESTful APIs adhere to the principles of REST, which include stateless communication, resource-based endpoints, and a uniform interface.

9. **GraphQL:**
   An alternative to REST, GraphQL is a query language and runtime for APIs that allows clients to request only the data they need. It provides more flexibility and efficiency in fetching data compared to traditional RESTful APIs.

10. **Webhooks:**
    Some APIs support webhooks, which are mechanisms that allow one system to notify another system about events or updates in real-time. This enables more proactive and event-driven interactions between applications.

In summary, APIs act as intermediaries that enable different software systems to interact and share data, facilitating the development of robust and interconnected applications. They are essential for creating a diverse and collaborative software ecosystem, where developers can leverage existing services and build upon each other's work.

## Fetching data from an API
### `XMLHttpRequest`
`XMLHttpRequest` is a built-in class in JavaScript. It is the traditional way of making HTTP requests in web browsers. The XMLHttpRequest object provides a way to interact with servers using HTTP or HTTPS to send and receive data.

`XMLHttpRequest` is an older way of making HTTP requests in JavaScript and was commonly used before the Fetch API was introduced. It is still supported in modern browsers for backward compatibility, but the Fetch API is considered more modern and is often preferred due to its simpler syntax and promises-based approach.

Here's a basic example of using `XMLHttpRequest` to fetch data from an API:

```javascript
// Create a new XMLHttpRequest object
var xhr = new XMLHttpRequest();

// Configure it with the HTTP method (GET), the URL, and whether the request should be asynchronous
xhr.open('GET', 'https://api.example.com/data', true);

// Set up a callback function to handle the response
xhr.onload = function () {
  // Check if the request was successful (status code 200)
  if (xhr.status >= 200 && xhr.status < 300) {
    // Parse the response as JSON
    var data = JSON.parse(xhr.responseText);
    // Work with the data
    console.log(data);
  } else {
    // Handle errors
    console.error('HTTP error! Status:', xhr.status);
  }
};

// Set up a callback function to handle network errors
xhr.onerror = function () {
  console.error('Network error');
};

// Send the request
xhr.send();
```

While `XMLHttpRequest` is still avaliable, the Fetch API provides a more modern and flexible interface, particularly with the use of Promises and a simpler syntax. If you have the option, it's generally recommended to use the Fetch API for making HTTP requests in contemporary web development.

### The `Fetch` API
The Fetch API is a modern JavaScript API for making network requests (e.g., fetching resources from a server). It provides a more powerful and flexible way to work with HTTP requests compared to the older XMLHttpRequest. The `Fetch` API is `Promise` based, unlike the `XMLHttpRequest` API which is callback based.

Here's a detailed explanation of the Fetch API:

1. **Basics:**
   The Fetch API is designed around the `fetch()` function, which takes a URL as its argument and returns a Promise that resolves to the `Response` to that request.

   ```javascript
   fetch('https://api.example.com/data')
     .then(response => {
       // handle the response
     })
     .catch(error => {
       // handle errors
     });
   ```

2. **Handling Responses:**
   The `Response` object represents the response to the request. You can check the status of the response and parse the data using methods like `json()`, `text()`, or `blob()`.

   ```javascript
   fetch('https://api.example.com/data')
     .then(response => {
       if (!response.ok) {
         throw new Error(`HTTP error! Status: ${response.status}`);
       }
       return response.json(); // or response.text() or response.blob()
     })
     .then(data => {
       // handle the parsed data
     })
     .catch(error => {
       // handle errors
     });
   ```

3. **Headers:**
   You can customize the headers of the request by passing an optional configuration object as the second parameter to `fetch()`.

   ```javascript
   fetch('https://api.example.com/data', {
     headers: {
       'Content-Type': 'application/json',
       'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
     }
   })
   ```

4. **HTTP Methods:**
   By default, `fetch()` makes a GET request. You can specify other HTTP methods using the `method` option.

   ```javascript
   fetch('https://api.example.com/data', {
     method: 'POST',
     body: JSON.stringify({ key: 'value' }) // Include data in the request body
   })
   ```

5. **Handling POST Requests:**
   When making a POST request or any other request that includes a body, you need to provide the `body` option with the data to be sent.

   ```javascript
   fetch('https://api.example.com/data', {
     method: 'POST',
     headers: {
       'Content-Type': 'application/json'
     },
     body: JSON.stringify({ key: 'value' })
   })
   ```

The Fetch API offers a modern and more convenient way to handle network requests in JavaScript applications.

### CORS (Cross-Origin Resource Sharing)
Cross-Origin Resource Sharing (CORS) is a security feature implemented by web browsers to restrict web pages from making requests to a different domain than the one that served the web page. In order to access a resource on another domain, we need to provide a second parameter, an `options` object to the `fetch` function. Inside the options object, we need to set the "mod" property to "cors".

```js
fetch('url.url.com/api', {
  mode: 'cors'
});
```

If mode: 'cors' is absent (or set to the default 'same-origin'), the browser will not allow cross-origin requests. The browser enforces the same-origin policy by default for security reasons, which prevents web pages from making requests to a different domain than the one that served the web page.

When you include mode: 'cors' in the fetch options, the browser will make a CORS (Cross-Origin Resource Sharing) request. In a CORS request, the browser includes additional headers in the HTTP request, and the server at the target domain needs to respond with the appropriate CORS headers indicating whether the request is allowed or not.

If the server at the target domain responds with the necessary CORS headers and allows the request, the browser proceeds with the actual request. If the server doesn't respond with the appropriate CORS headers or denies the request, the browser will prevent the response from being accessed by the calling script, maintaining security and preventing unauthorized cross-origin requests.

### The `Headers` Interface
The `Headers` interface is used to represent and manipulate the headers associated with an HTTP request or response.

The `Headers` constructor can be used to create a new Headers object. Here's a basic example:

```javascript
// Creating a new Headers object
let headers = new Headers();

// Adding headers to the object
headers.append('Content-Type', 'application/json');
headers.append('Authorization', 'Bearer YOUR_ACCESS_TOKEN');

// You can also set headers using an object literal
// let headers = new Headers({'Content-Type': 'application/json', 'Authorization': 'Bearer YOUR_ACCESS_TOKEN'});
```

You can then use this `Headers` object when making a fetch request:

```javascript
fetch('https://example.com/api/data', {
  method: 'GET',
  headers: headers,
})
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

In this example, the `headers` object is passed as part of the configuration options in the `fetch` call. It allows you to include specific headers in your HTTP request.

You can also manipulate headers using various methods provided by the `Headers` interface, such as `append()`, `delete()`, `get()`, `set()`, etc. These methods allow you to add, remove, or retrieve headers from the `Headers` object.

Here's a quick example of using `append()` to add a new header:

```javascript
headers.append('Accept-Language', 'en-US');
```

This adds the 'Accept-Language' header to the existing headers.

### The `Request` Interface
The `Request` object represents an HTTP request. It is used to configure and provide information about the request that you want to make using the `fetch` function. Instead of passing a path to the resource you want to request into the fetch() call, you can create a request object using the Request() constructor, and pass that in as a fetch() method argument.

The `Request` constructor allows you to create a new `Request` object, specifying details such as the URL, method, headers, and other request-specific parameters. Once you have a `Request` object, you can pass it to the `fetch` function to make the actual HTTP request.

Here's a basic example:

```javascript
// Creating a new Request object
let request = new Request('https://example.com/api/data', {
  method: 'GET',
  headers: new Headers({
    'Content-Type': 'application/json',
    'Authorization': 'Bearer YOUR_ACCESS_TOKEN'
  }),
  mode: 'cors', // specify the mode (e.g., 'cors', 'no-cors', 'same-origin')
  cache: 'default' // specify the caching behavior (e.g., 'default', 'no-store', 'reload')
});

// Making the HTTP request using fetch
fetch(request)
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error('Error:', error));
```

In this example:

- The `Request` object is created with the URL ('https://example.com/api/data') and an options object specifying the HTTP method ('GET'), headers, mode, and cache behavior.
- The `fetch` function is then used to make the actual HTTP request, passing the `Request` object as an argument.

The `Request` interface provides various options that you can include in the configuration object:

- `method`: The HTTP method (e.g., 'GET', 'POST', 'PUT', etc.).
- `headers`: An object or `Headers` instance representing the headers associated with the request.
- `mode`: The mode of the request (e.g., 'cors', 'no-cors', 'same-origin'). This determines how cross-origin requests are handled.
- `cache`: The caching behavior of the request (e.g., 'default', 'no-store', 'reload').
- `redirect`: The follow-redirect mode (e.g., 'follow', 'error', 'manual').
- `referrer`: The referrer of the request (e.g., 'no-referrer', 'no-referrer-when-downgrade').
- ...and more.

### The `Response` API
When you make a request using the Fetch API, it returns a Promise that resolves to the `Response` object representing the response to the request. The `Response` interface provides various methods and properties to access the response data and metadata.

You can create a new Response object using the Response() constructor, but you are more likely to encounter a Response object being returned as the result of another API operation—for example, a service worker FetchEvent.respondWith, or a simple fetch().

Here's a detailed explanation of the `Response` interface:

 **Instance Properties:**

1. **`Response.url`**:
   - A string representing the URL of the response.
  
2. **`Response.type`**:
   - A string indicating the type of the response (e.g., "basic", "cors", "opaque", "error", or "opaqueredirect").
  
3. **`Response.ok`**:
   - A boolean indicating whether the response was successful (status in the range 200-299) or not.

4. **`Response.status`**:
   - An integer representing the HTTP status code of the response.

5. **`Response.statusText`**:
   - A string representing the status message associated with the status code of the response.

6. **`Response.headers`**:
   - A Headers object representing the headers of the response.

**Instance Methods:**

1. **`Response.clone()`**:
   - Creates a clone of the `Response` object. This is useful when you want to consume the body of the response more than once.

2. **`Response.arrayBuffer()`**:
   - Returns a promise that resolves with an ArrayBuffer representing the response body.

3. **`Response.blob()`**:
   - Returns a promise that resolves with a Blob representing the response body.

4. **`Response.formData()`**:
   - Returns a promise that resolves with a FormData object representing the response body.

5. **`Response.json()`**:
   - Returns a promise that resolves with a JSON object representing the response body.

6. **`Response.text()`**:
   - Returns a promise that resolves with a text representation of the response body.

**Example Usage:**

```javascript
fetch('https://api.example.com/data')
  .then(response => {
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    return response.json();
  })
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error('Fetch error:', error);
  });
```

The Response object does not directly contain the actual JSON response body but is instead a representation of the entire HTTP response. So, to extract the JSON body content from the Response object, we use the `json()` method, which returns a second promise that resolves with the result of parsing the response body text as JSON.

### Checking that the fetch was successful
A fetch() promise will reject with a TypeError when a network error is encountered or CORS is misconfigured on the server-side, although this usually means permission issues or similar — a 404 does not constitute a network error, for example. An accurate check for a successful fetch() would include checking that the promise resolved, then checking that the Response.ok property has a value of true. The code would look something like this:

```js
async function fetchImage() {
  try {
    const response = await fetch("flowers.jpg");
    if (!response.ok) {
      throw new Error("Network response was not OK");
    }
    const myBlob = await response.blob();
    myImage.src = URL.createObjectURL(myBlob);
  } catch (error) {
    console.error("There has been a problem with your fetch operation:", error);
  }
}
```

---
### Knowledge Check

**Q1.** What is an API?

**A1.** An API, or Application Programming Interface, is a set of rules and tools that allows different software applications to communicate with each other. It serves as a bridge between different software systems, enabling them to exchange information and perform specific tasks seamlessly. APIs play a crucial role in modern software development, fostering interoperability and enabling the creation of more powerful and complex applications by leveraging the capabilities of existing services and libraries.

**Q2.** How is access to an API restricted?

**A2.** Access to an API (Application Programming Interface) is typically restricted and controlled to ensure security, manage resources, and protect the API provider's infrastructure. There are several common methods for restricting API access:

1. **API Keys:** API keys are unique identifiers that developers must include in their API requests. The API provider issues these keys to developers during the registration process. This method is simple but may not be as secure as other options.

2. **Authentication Tokens:** Instead of API keys, some APIs use authentication tokens, which are more secure and provide additional features like expiration dates and scope limitations. Common token-based authentication methods include OAuth and JWT (JSON Web Tokens).

3. **OAuth (Open Authorization):** OAuth is a widely used authentication and authorization protocol. It allows users to grant third-party applications limited access to their resources without exposing credentials. OAuth 2.0 is the latest version and is commonly used for web and mobile applications.

4. **IP Whitelisting/Blacklisting:** APIs can be configured to only accept requests from specific IP addresses (whitelisting) or block requests from specific IP addresses (blacklisting). This helps control the source of incoming API requests.

5. **Rate Limiting:** To prevent abuse or excessive usage, APIs often implement rate limiting. This involves restricting the number of requests a client can make within a specified time period. Developers may need to upgrade their API access level to get a higher rate limit.

6. **HTTP Referrer Checking:** APIs may check the HTTP referrer header to ensure that requests are coming from an authorized source, such as a specific domain.

7. **Client Certificates:** For more robust security, APIs can require clients to present a valid client certificate during the SSL/TLS handshake. This is often used in situations where a higher level of security is necessary.

API providers often use a combination of these methods to create a layered and secure access control system. The specific method chosen depends on the nature of the API, the sensitivity of the data it exposes, and the level of security required.

**Q3.** How do you fetch and extract data from an API?

**A3.** We can use the `Fetch` API to fetch(GET) data from an API. The Fetch API is a modern JavaScript API for making network requests (e.g., fetching resources from a server). It provides a more powerful and flexible way to work with HTTP requests compared to the older XMLHttpRequest. The `Fetch` API is `Promise` based, unlike the `XMLHttpRequest` API which is callback based.

1. **Basics:**
   The Fetch API is designed around the `fetch()` function, which takes a URL as its argument and returns a Promise that resolves to the `Response` to that request.

   ```javascript
   fetch('https://api.example.com/data')
     .then(response => {
       // handle the response
     })
     .catch(error => {
       // handle errors
     });
   ```

2. **Handling Responses:**
   The `Response` object represents the response to the request. You can check the status of the response and parse the data using methods like `json()`, `text()`, or `blob()`.

   ```javascript
   fetch('https://api.example.com/data')
     .then(response => {
       if (!response.ok) {
         throw new Error(`HTTP error! Status: ${response.status}`);
       }
       return response.json(); // or response.text() or response.blob()
     })
     .then(data => {
       // handle the parsed data
     })
     .catch(error => {
       // handle errors
     });
   ```

**Q4.** Why might your API request be blocked by the browser, and how might you fix this?

**A4.** Cross-Origin Resource Sharing (CORS) is a security feature implemented by web browsers to restrict web pages from making requests to a different domain than the one that served the web page. In order to access a resource on another domain, we need to provide a second parameter, an `options` object to the `fetch` function. Inside the options object, we need to set the "mod" property to "cors".

```js
fetch('url.url.com/api', {
  mode: 'cors'
});
```

If mode: 'cors' is absent (or set to the default 'same-origin'), the browser will not allow cross-origin requests. The browser enforces the same-origin policy by default for security reasons, which prevents web pages from making requests to a different domain than the one that served the web page.

When you include mode: 'cors' in the fetch options, the browser will make a CORS (Cross-Origin Resource Sharing) request. In a CORS request, the browser includes additional headers in the HTTP request, and the server at the target domain needs to respond with the appropriate CORS headers indicating whether the request is allowed or not.

If the server at the target domain responds with the necessary CORS headers and allows the request, the browser proceeds with the actual request. If the server doesn't respond with the appropriate CORS headers or denies the request, the browser will prevent the response from being accessed by the calling script, maintaining security and preventing unauthorized cross-origin requests.
