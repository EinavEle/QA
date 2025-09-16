##### *Intro*
HTTP requests are a way to ask a web server for information or resources, like when you type in a URL in your browser. 
They usually include a method (like GET or POST), a URL, and headers with extra information. 
You can also include data in the request body. 
In Java, you can send HTTP requests using libraries like HttpURLConnection, Apache HttpClient, or OkHttp, which make it easier to work with requests and responses.
In our BootCamp we will work with Apache HttpClient.

#### *Apache HTTP Client*
Apache HttpClient is a library in Java that makes it easier to send and receive HTTP requests and responses. 
It provides a higher-level abstraction over the low-level HttpURLConnection class, allowing developers to write cleaner, more concise code for working with HTTP.

With Apache HttpClient, you can send requests using various HTTP methods like GET, POST, PUT, and DELETE, and include headers and request bodies as needed. 
The library also includes features for handling redirects, cookies, and authentication.

In addition, Apache HttpClient provides options for configuring connection settings, such as timeouts and proxy settings, and for controlling the behavior of SSL/TLS connections.

Overall, Apache HttpClient is a powerful and flexible library for working with HTTP requests and responses in Java applications, and is widely used in many different types of projects.

For example:
```Java
public static void simpleGetRequest() throws IOException {
    HttpClient client = HttpClientBuilder.create().build();
    HttpGet request = new HttpGet("https://api.publicapis.org/entries");
    request.addHeader("Accept-Language", "en-US");
    request.addHeader("User-Agent", "Mozilla/5.0");
    HttpResponse response = client.execute(request);
    System.out.println("Response Code : " +
                                response.getStatusLine().getStatusCode());
    String responseBody = EntityUtils.toString(response.getEntity());
    System.out.println("Response Body : " + responseBody);
}
```

#### *Request & Response Entities*
**Json schema**
JSON Schema is a way to describe and validate the structure and content of JSON data. It's like a contract that defines what properties should be present, their types, and any additional rules. 
It helps ensure that JSON data follows a specific format and meets certain requirements. JSON Schema is used for data validation, documentation, generating sample data, and mapping data between different JSON structures. It promotes interoperability and makes it easier to work with JSON.

Similarly, when you send data to an API (such as creating a new user account), the API might use a JSON Schema to validate that the data you send is in the correct format and contains all the required fields.

In short, JSON Schema helps ensure that the data exchanged between web applications follows a certain structure and can be easily processed.

For example:
```Java
{
  "type": "object",
  "properties": {
    "location": {
      "type": "string"
    },
    "time": {
      "type": "string",
      "format": "date-time"
    },
    "temperature": {
      "type": "number"
    },
    "description": {
      "type": "string"
    }
  },
  "required": [
    "location",
    "time",
    "temperature",
    "description"
  ]
}
```
The schema specifies that the data should be an object with four properties: location, time, temperature, and description. 
The location property should be a string, the time property should be a string in date-time format, the temperature property should be a number, and the description property should be a string. 
The required keyword specifies that all four properties are required in the data.

**Lombok**
Lombok is a Java library that helps reduce boilerplate code in Java classes. 
It provides annotations that can be used to generate getters, setters, constructors, equals, hashCode, and toString methods automatically, based on the fields in the class.

By using Lombok, you can write more concise and readable code, without sacrificing the readability of the generated code. 
This can help improve the maintainability and readability of your codebase, and reduce the time and effort required to write and maintain classes.

Since the entities we work with in requests and responses can be very long depending on the amount of fields returned, we would like to work with Lombok which will significantly shorten our code and save us getters, setters and constructors

For example, with Lombok, you can annotate a class with @Data to generate getters, setters, equals, hashCode, and toString methods automatically, like this:
```Java
import lombok.Data;
@Data
public class SimpleRequest {
    public String country;
}
```
This will generate the following code:
```Java
public class SimpleRequestWitoutLombok {
    public String country;
    public SimpleRequestWitoutLombok(String country) {
        this.country = country;
    }
    public String getCountry() {
        return country;
    }
    public void setCountry(String country) {
        this.country = country;
    }
    @Override
    public String toString() {
        return "SimpleRequestWitoutLombok{" +
                "country='" + country + '\'' +
                '}';
    }
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (o == null || getClass() != o.getClass()) return false;
        SimpleRequestWitoutLombok that = (SimpleRequestWitoutLombok) o;
        return country.equals(that.country);
    }
    @Override
    public int hashCode() {
        return Objects.hash(country);
    }
}
```
This can save a lot of time and effort, especially for classes with many fields, while still maintaining readability and clarity in the generated code.

**Static Factories**
Static factories are like shortcut methods that can create objects of request and response entities in web development. They are declared as static methods, which means they don't require an instance of the class to be created.

Using static factories, you can create objects of request and response entities with more descriptive names and based on different input parameters. For example, you can have a factory method called "fromUrl" that creates an HTTP request object from a URL string or a method called "ok" that creates an HTTP response object with a successful status code.

Overall, static factories can make it easier and more readable to create objects of request and response entities in web development.

For example:
```Java
public class HttpRequest {
    private String method;
    private String url;
    private Map<String, String> headers;
    private String body;
    private HttpRequest(String method, String url,
                           Map<String, String> headers, String body) {
        this.method = method;
        this.url = url;
        this.headers = headers;
        this.body = body;
    }
    public static HttpRequest fromUrl(String url) {
        Map<String, String> headers = new HashMap<>();
        headers.put("Content-Type", "text/html");

        return new HttpRequest("GET", url, headers, null);
    }
}
```
In this example, the “HttpRequest” class has  static factory methods  “fromUrl”
The “fromUrl” method takes a URL string as input, creates a new “HttpRequest” object with the HTTP method "GET", sets the URL to the input URL, sets the headers to a default value, and sets the body to null.

Using these static factory methods, you can create instances of the HttpRequest class with different parameters in a more convenient and readable way. 

For example:
```Java
HttpRequest request = HttpRequest.fromUrl("https://api.publicapis.org/entries");
```

**Builder pattern**
The Builder pattern is a way to create complex objects by breaking down the construction process into multiple steps. 
It's useful for creating request entities that have multiple properties, some of which may be optional.

In our example we define a PersonRequest class with a Builder pattern for creating objects with required and optional parameters. 
The builder class initializes the required parameters and allows the optional parameters to be set through a chain of method calls. The build method creates a new PersonRequest object with the specified parameters.

Code example:
```Java
public class PersonRequest {
    private final int id;
    private final String firstName;
    private final String lastName;
    private String phone;
    private String address;
    private double height;
    private double weight;
    private int age;

    public static class Builder {
        //Required Parameters
        private final int id;
        private final String firstName;
        private final String lastName;

        //Optional Parameters
        private String phone = "123-456-789";
        private String address = "Street 1, City";
        private double height = 1.70;
        private double weight = 75.5;
        private int age = 30;

        public Builder(int id, String firstName, String lastName) {
            this.id = id;
            this.firstName = firstName;
            this.lastName = lastName;
        }

        public Builder phone(String phone) {
            this.phone = phone;
            return this;
        }

        public Builder address(String address) {
            this.address = address;
            return this;
        }

        public Builder height(double height) {
            this.height = height;
            return this;
        }

        public Builder weight(double weight) {
            this.weight = weight;
            return this;
        }

        public Builder age(int age) {
            this.age = age;
            return this;
        }

        public PersonRequest build() {
            return new Person(this);
        }
    }

    private PersonRequest(Builder builder) {
        this.id = builder.id;
        this.firstName = builder.firstName;
        this.lastName = builder.lastName;
        this.phone = builder.phone;
        this.address = builder.address;
        this.height = builder.height;
        this.weight = builder.weight;
        this.age = builder.age;
    }
}
```
To use this code, you would first create a new instance of the Builder class and pass in the required parameters (id, firstName, and lastName) to the builder constructor. Then, you could chain optional parameter methods to set any additional parameters you want to include. Finally, you would call the build method to create a new PersonRequest object with the specified parameters. Here's an example:
```Java
PersonRequest personRequest = 
                            new PersonRequest.Builder(123, "Tzahi", "Anidgar")
    .phone("052-8635700")
    .address("HaMelacha 5, Netanya")
    .age(36)
    .build();
```
This creates a new PersonRequest object with the required parameters of id=123, firstName="Tzahi", and lastName="Anidgar", and optional parameters of phone="052-8635700", address="HaMelacha 5, Netanya", and age=36.

Using the Builder pattern can make your code more readable and easier to modify in the future. 
It also allows you to add new properties without changing the client code.

# *HTTP Util Facade*
The HTTP Util Facade is a design pattern that simplifies making HTTP requests to remote servers. It provides a set of functions that hide the low-level details of managing connections, handling timeouts and retries, and parsing response data.

For example, a Java implementation of an HTTP Util Facade might include functions for GET, POST, PUT, and DELETE requests. 
These functions take a URL and optional parameters such as headers, query parameters, and request body, and return a response object containing the status code, headers, and response body.

Using an HTTP Util Facade can make your code more modular, easier to test, and easier to read by providing a consistent way of making HTTP requests throughout your application.

Here example for HttpUtil with GET request:
```Java
public static HttpResponse get(String url, Map<String, String> headers,
                        Map<String, String> queryParams) throws IOException 
{
    // create connection
    HttpURLConnection connection = 
                        (HttpURLConnection) new URL(url).openConnection();
    connection.setRequestMethod("GET");
    // set headers
    for (Map.Entry<String, String> entry : headers.entrySet()) {
        connection.setRequestProperty(entry.getKey(), entry.getValue());
    }
    // set query parameters
    if (queryParams != null) {
        String queryString = queryParams.entrySet().stream()
                .map(entry -> entry.getKey() + "=" + entry.getValue())
                .collect(Collectors.joining("&"));
        url += "?" + queryString;
    }
    // send request and handle response
    int status = connection.getResponseCode();
    String body = new String(connection.getInputStream().readAllBytes());
    Map<String, String> responseHeaders =
                      connection.getHeaderFields().entrySet()
                      .stream()
                      .filter(entry -> entry.getKey() != null)
                      .collect(Collectors.toMap(Map.Entry::getKey, entry ->
                                                entry.getValue().get(0)));
    return new HttpResponse(status, responseHeaders, body);
    }
    // similar functions for other HTTP methods
}
```
This code is a function that sends an HTTP GET request to a URL with optional headers and query parameters, and returns the HTTP response as an object. 
The function takes three arguments: the URL to send the request to, a map of headers to include in the request, and a map of query parameters to include in the request.

Inside the function, the code creates an HTTP connection using the given URL, sets the request method to GET, and adds any headers specified in the input. 
If query parameters are specified, they are added to the URL.

The code then sends the request and gets the response status code, headers, and body. These are combined into an HttpResponse object, which is returned by the function.

This function is part of a larger set of similar functions for sending HTTP requests using other HTTP methods like POST, PUT, and DELETE.

# Wrapping API Responses
A response wrapper is used to standardize the format of API responses, making them more consistent and easier to handle by clients. 
It also allows for additional information to be added to the response, such as metadata or error messages.

To implement a response wrapper in Apache Java, you can create a class that represents the response and includes the actual data as well as any additional information. For example:
```Java
public class HttpResponse<T> {
    private int status;
    private Map<String, String> responseHeaders;
    private T data;
    public HttpResponse(int status, Map<String, String> responseHeaders, 
                                                                       T data)
 {
        this.status = status;
        this.responseHeaders = responseHeaders;
        this.data = data;
    }
 // getters and setters
}
```
In this example, the HttpResponse class takes a generic type T to represent the type of data being returned. 
It also includes a success flag to indicate whether the API call was successful, and a message field to include any additional information.

You can then use this HttpResponse class to wrap the actual data being returned by the API. For example:
```Java
public HttpResponse<User> getUserById( Long id) {
    User user = userRepository.findById(id).orElse(null);

    if (user != null) {
        return new HttpResponse<>(user, true, "User found");
    } else {
        return new HttpResponse<>(null, false, "User not found");
    }
}
```
In this example, the getUserById method returns an HttpResponse object wrapping the User object being returned by the userRepository.
The success flag and message fields are set based on whether the user was found or not.

By using a response wrapper like HttpResponse, you can provide a standardized format for API responses and make them easier to handle by clients.