Using our example of HTTP GET method, write a method that executes a POST request.
Use it to create a new using in this API: https://reqres.in/
Use the response wrappers in our example to get the result.
<details>
  <summary>
     Solution
  </summary>

```Java 
public static HttpResponse post(String url, Map<String, String> headers,
                                              String body) throws IOException {
        // create connection
        HttpURLConnection connection = 
                          (HttpURLConnection) new URL(url).openConnection();
        connection.setRequestMethod("POST");
        connection.setDoOutput(true);
        // set headers
        for (Map.Entry<String, String> entry : headers.entrySet()) {
            connection.setRequestProperty(entry.getKey(), entry.getValue());
        }
        // send request body
        OutputStream os = connection.getOutputStream();
        os.write(body.getBytes());
        os.flush();
        os.close();
        // handle response
        int status = connection.getResponseCode();
        String responseBody = "";
        if (status >= 200 && status < 300) {
            responseBody = 
                    new String(connection.getInputStream().readAllBytes());
        } else {
            responseBody = 
                     new String(connection.getErrorStream().readAllBytes());
        }

        Map<String, String> responseHeaders = new HashMap<>();
        for (Map.Entry<String, List<String>> entry :
                            connection.getHeaderFields().entrySet()) {
            if (entry.getKey() != null) {
                responseHeaders.put(entry.getKey(), entry.getValue().get(0));
            }
        }
        return new HttpResponse(status, responseHeaders, responseBody);
    }
}
```

</details>