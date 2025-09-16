You must write at least 3 API tests for the following:

https://wizard-world-api.herokuapp.com/swagger/index.html

At least one test must have a post.
<details>
  <summary>
     Solution
  </summary>

1. To check if the API's response is what you expected.
1. To confirm if the API response matches your expectations.
1. To check if an API does what it's supposed to do.


1. 
    ```Postman
    GET https://wizard-world-api.herokuapp.com/Houses/
    ```
    Body:
    {
        "id":"3fa85f64-5717-4562-b3fc-2c963f66afa6"
    }
    Response:
      Status: 200 OK
1. 
    ```Postman
    GET https://wizard-world-api.herokuapp.com/Houses/036f3-1cb6-4baf-bede-48e17e1cd005
    ```
    Response
    ```Postman
    {
        "errors": {
            "id": [
                "The value '036f3-1cb6-4baf-bede-48e17e1cd005' is not valid."
            ]
        },
        "type": "https://tools.ietf.org/html/rfc7231#section-6.5.1",
        "title": "One or more validation errors occurred.",
        "status": 400,
        "traceId": "00-60e11a6a5fc4f24d99f64b88916e52ba-4e66cba563f7304b-00"
    }
    ```
1. 
    ```Postman
    POST "https://wizard-world-api.herokuapp.com/Feedback"
    ```
    ```Postman
    {
      "feedbackType": "General",
      "feedback": "string",
      "entityId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
    }
    ```
    Response:
    Status: 200 OK

</details>