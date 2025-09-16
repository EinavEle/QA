API Validations can be done on both the request and response of an API. 
Response validation involves checking two things: status and data.

Status validation confirms if the HTTP status code returned by the API after a request is successful, failed, or encountered an error. 
HTTP status codes are three-digit numbers that show the status of the request.
For example from the example of the Harry Potter house test:
```Java
Assert.assertEquals(result.getStatus(),200);
```
Data validation, on the other hand, checks the data returned by the API in response to a request. 
It verifies whether the data is in the expected format and content. 
For instance, if an API is supposed to return JSON data, data validation checks if the JSON has the expected fields and values.

For example from the Harry Potter house test:
```Java
Assert.assertEquals(result.getData().getId(),HarryPotterHouses.GRYFFINDOR.id); Assert.assertEquals(result.getData().getName(),HarryPotterHouses.
                                                             GRYFFINDOR.name);
```
Here we check the data that returns in our case the ID and the house name.

By performing API Validations on the response, developers can ensure that the API returns accurate results. 
This helps to improve the reliability and quality of the API.