# *Intro*
REST API methods are used to perform operations on resources over the HTTP protocol. These methods provide a standardized way to interact with RESTful web services and enable clients to perform various CRUD (Create, Read, Update, Delete) operations on resources.
# *Methods*
**GET**
Used to retrieve data from the server. 
For example, a GET request to https://api.example.com/products would retrieve a list of products.
```java
GET http://example.com/products
```
**POST**
Used to send data to the server to create a new resource. For example, a POST request to https://api.example.com/products with a JSON body containing product information would create a new product.
```java
POST http://example.com/products 
Content-Type: application/json
Body: {
  "name": "John Doe",
  "price": "100"
}
```
**PUT**
Used to send data to the server to update an existing resource. 
For example, a PUT request to https://api.example.com/products/123 with a JSON body containing updated product information would update the product with ID 123.
```java
PUT http://example.com/products/123 
Content-Type: application/json
Body: {
  "name": "Jane Doe",
  "price": "500"
}
```
**PATCH**
Used to send data to the server to update parts of an existing resource. 
For example, a PATCH request to https://api.example.com/products/123 with a JSON body containing updated product information would update only the specified fields of the product with ID 123.
```java
PATCH /products/123
Content-Type: application/json-patch+json
Body: [
  { "op": "replace", "path": "/name", "value": "Jane Doe" }
]
```
**DELETE**
Used to delete a resource from the server. 
For example, a DELETE request to https://api.example.com/products/123 would delete the product with ID 123 from the server.
```java
DELETE /products/123 
```
**OPTIONS**
Used to retrieve information about the communication options available for a resource. For example, an OPTIONS request to https://api.example.com/products would retrieve the available methods that can be used on the products resource.
```java
OPTIONS /users
```
Example Response:
```java
HTTP/1.1 200 OK
Allow: GET, POST
Access-Control-Allow-Origin: *
Access-Control-Allow-Methods: GET, POST
Access-Control-Allow-Headers: Authorization, Content-Type
Content-Length: 0
```