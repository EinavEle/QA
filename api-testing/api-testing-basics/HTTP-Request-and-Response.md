# *Intro*
Intro
HTTP is the underlying protocol used to transfer data between clients and servers on the World Wide Web.
When a client wants to request information or perform an action on a web server, it sends an HTTP request to the server. 
The server responds to the request with an HTTP response.

# *Structure*
**An HTTP request typically consists of the following parts:**
- Method: Specifies the type of request being made, such as GET or POST.
- URL: Specifies the location of the resource being requested.
- Headers: Provide additional information about the request, such as the type of data being sent.
- Body: Contains any data being sent with the request, such as form data.
```java
Request URL: https://wizard-world-api.herokuapp.com/Feedback
Request Method: POST
Headers:
    accept: text/plain
    Accept-Encoding: gzip, deflate, br
    Accept-Language: en-US,en;q=0.9
    Connection: keep-alive

Body:
{
  "feedbackType": "General",
  "feedback": "string",
  "entityId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
}
```
*In this example, only some of the headers appear

**An HTTP response typically consists of the following parts:**
- Status code: Specifies the status of the response, such as whether the request was successful or not.
- Headers: Provide additional information about the response, such as the type of data being returned.
- Body: Contains the data being returned by the server, such as the content of a webpage or the result of an API call.
```java
Status Code: 200 OK
Headers:
Host: example.com
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6
Content-Type: application/json
Connection: keep-alive
Date: Mon, 10 Apr 2023 13:33:40 GMT
Content-Type: application/json; charset=utf-8
Server: Kestrel
Content-Length: 2
Access-Control-Allow-Origin: *
Via: 1.1 vegur
Body:
{
  "id": "0106fb32-b00d-4d70-9841-4b7c2d2cca71",
  "name": "Fergus Fungal Budge",
  "effect": "Treats ringworm, fungicide",
  "sideEffects": "Potential negative side effects if used by elves",
  "characteristics": null,
  "time": null,
  "difficulty": "Unknown",
  "ingredients": [
    {
      "id": "4ff5aaf2-776f-43c6-9896-c79c67dc90c5",
      "name": "Neem oil"
    },
    {
      "id": "846be123-c40f-4156-91f4-800305df7485",
      "name": "Jewelweed"
    },
    {
      "id": "a08e7390-a362-4013-b413-11b151fae20e",
      "name": "Onion juice"
    }
  ],
  "inventors": [],
  "manufacturer": null
}
```
HTTP requests and responses are the building blocks of communication between clients and servers on the web. 
By using these standardized formats, different clients and servers can communicate with each other regardless of the technologies they use.
# *Types of Arguments*
When working with APIs, there are different types of arguments that can be used to send and receive data between clients and servers. 

Here are three common types:
1. Query Parameters: Query parameters are used to filter or paginate data in a request. They are added to the end of a URL and are separated by a question mark. 
For example, a query parameter in a weather API might look like this: http://api.weather.com/forecast?location=NewYork.
    ```java
    GET http://api.weather.com/forecast?location=NewYork
    ```
1. Path Variables: Path variables are used to identify a specific resource in a URL. 
They are included in the URL itself and are indicated by curly braces {}.
For example, a path variable in a blog API might look like this: http://api.myblog.com/posts/{postID}.
    ```java
    DELETE http://api.myblog.com/posts/123
    ```
1. Request Body: The request body is used to send data to the server in a request. 
It is typically used when creating or updating a resource. 
The data is sent in the body of the request in a specific format, such as JSON or XML. For example, in a user registration API, the request body might include data like a user's name and email address.
```java
{
  "userName": "userTest",
  "email": "automationUserTerst@gotech.io",
}
```
By understanding the different types of arguments, developers can choose the best approach for their specific use case and build more effective and efficient APIs.

# *Response Statuses*
When a client sends a request to a server using an API, the server responds with a status code that indicates the status of the request. 

Response statuses are standardized codes that allow clients to understand the outcome of their requests.

There are several different response status codes, ranging from informational codes like 100 to error codes like 500, They are divided into groups according to the following explanation:
100 group: Items in progress.
200 group: Successful responses.
300 group: Redirects, which tell the browser to look someplace else.
400 group: Client errors.
500 group: Server errors.

Some of the most common response status codes include:
1. **200 OK**: Indicates that the request was successful and the server is returning the requested data.
1. **201 Created**: Indicates that the server has successfully created a new resource as a result of the request.
1. **400 Bad Request**: Indicates that the server was unable to process the request due to invalid syntax or missing data in the request.
1. **401 Unauthorized**: Indicates that the client needs to provide authentication credentials to access the requested resource.
1. **404 Not Found**: Indicates that the server was unable to find the requested resource.
1. **500 Internal Server Error**: Indicates that an error occurred on the server while processing the request.

By understanding response statuses, developers can troubleshoot issues with their APIs and ensure that clients are receiving the expected results from their requests.