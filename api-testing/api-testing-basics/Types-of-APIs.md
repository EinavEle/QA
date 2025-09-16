There are three main types of APIs: SOAP, REST, and GraphQL.
# *SOAP*
SOAP(Simple Object Access Protocol ) is a messaging protocol that uses XML to transfer data between different systems. It defines a strongly typed messaging framework and explicitly defines the structure of the request and response for each operation.

SOAP is a bit of a complex one - it uses a bunch of different standards to send structured information between different systems. 
It's not as popular as it used to be, because it can be a bit slower and more resource-intensive than other APIs.

A good example of a SOAP API is the Amazon Product Advertising API. 
This API allows developers to access Amazon's product database and retrieve information about specific products, such as their price, availability, and customer reviews. 
The API uses SOAP to exchange structured data between the Amazon server and the developer's application.

Here is an example for request and response:
**Request**
```SOAP
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:ns="http://example.com/api">
   <soap:Header/>
   <soap:Body>
      <ns:GetUserInfo>
         <ns:Username>john_doe</ns:Username>
      </ns:GetUserInfo>
   </soap:Body>
</soap:Envelope>
```
**Response**
```SOAP
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope" xmlns:ns="http://example.com/api">
   <soap:Header/>
   <soap:Body>
      <ns:GetUserInfoResponse>
         <ns:User>
            <ns:Name>John Doe</ns:Name>
            <ns:Email>john.doe@example.com</ns:Email>
            <ns:Role>Admin</ns:Role>
         </ns:User>
      </ns:GetUserInfoResponse>
   </soap:Body>
</soap:Envelope>
```
# *REST*
REST is probably the most common API you'll come across. It's designed to be lightweight and easy to use. 
Basically, you send a request to the API using HTTP (Hypertext Transfer Protocol)(like a message), and it sends back the data you asked for in JSON format (a type of text format that's easy for computers to read). REST is "stateless", meaning that it doesn't need to remember any context or details about your session in order to work.

One popular REST API is the Twitter API. 
This API allows developers to retrieve tweets, post new tweets, and perform other actions related to Twitter. 
Developers can use HTTP requests to access the API and receive data in JSON format. 
For example, a developer could use the Twitter API to retrieve all tweets that contain a specific hashtag or keyword.

Here is an example of request and response:
**Request**
```REST
GET /api/users/john_doe HTTP/1.1
Host: example.com
Accept: application/json
```
**Response**
```REST
{
  "name": "John Doe",
  "email": "john.doe@example.com",
  "role": "Admin"
}
```

# *GraphQL*
GraphQL is a newer type of API that was developed by Facebook. 
It's similar to REST in that you can send requests over HTTP and get data back in JSON format. But with GraphQL, you can be really specific about the data you want - you don't get everything, just what you ask for. 
This can make things faster and more efficient, especially if you're working with lots of data.

An example of a GraphQL API is the GitHub GraphQL API. 
This API allows developers to retrieve data about GitHub repositories, users, and organizations. 
Unlike a REST API, the GitHub GraphQL API allows developers to specify exactly what data they want to retrieve, making it more efficient and flexible. 
For example, a developer could use the GitHub GraphQL API to retrieve all the pull requests associated with a specific repository.

Here is an example of request and response:
**Request**
```GraphQL
POST /graphql HTTP/1.1
Host: example.com
Content-Type: application/json

{
  "query": "query GetUser($username: String!) { user(username: $username) { name email role } }",
  "variables": {
    "username": "john_doe"
  }
}
```
**Response**
```GraphQL
{
  "data": {
    "user": {
      "name": "John Doe",
      "email": "john.doe@example.com",
      "role": "Admin"
    }
  }
}
```
Each of these APIs has its own pros and cons, so it's important to choose the right one for your needs. The main thing is to make sure your API is reliable, fast, and easy to use.
