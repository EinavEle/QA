# How get data from response(In clint)
To get data from a response in Playwright TypeScript, you can use the waitForResponse method to intercept the network request and then use the json() method on the response object to extract the JSON data from the response.

Here's an example of how to do it:

```Playwright
  test('Get data from response',async ({ page }) => {
        // Wait for the response from the specified URL and intercept it
        const responsePromise = page.waitForResponse
                   ('https://cat-fact.herokuapp.com/facts?animal_type=snail');
        //Go to the page where the request is call
        await page.goto('https://cat-fact.herokuapp.com/#/snail/facts')
        //wait to the results
        const response = await responsePromise
        // Get the JSON data from the response
        const dataResponse = await response.json();
        // Perform assertions or any other actions with the extracted data
        expect(dataResponse[0]["_id"]).toBe('58e008780aac31001185ed05');
      });
```

In this example, we first use waitForResponse to wait for the response from the specified URL (in this case, the API endpoint for snail facts). 
Next, we navigate to the url and use this request and wait for the response. 
Then we use response.json() to parse the JSON data from the response. 
The extracted JSON data is then stored in the dataResponse variable.

Finally, you can perform any necessary actions with the dataResponse, making assertions to verify specific data elements, as shown in the example using expect.

# Making API requests
In order to read the requests or send the customized body, we can export a Playwright object and use its built-in methods, when we make a request that returns an answer with a body, we can receive it as an object of APIRespones and we can work with it

Attached are examples of applications in response and request
```Playwright
 test(`use response data`, async ({ request }) => {
        const getResult = await 
                 request.get(`https://wizard-world-api.herokuapp.com/Elixirs
                                      /0106fb32-b00d-4d70-9841-4b7c2d2cca71`);
        const body = await getResult.json()
        expect(body['id']).toBe("0106fb32-b00d-4d70-9841-4b7c2d2cca71")
        expect(getResult.ok()).toBeTruthy();
    })
```
In this example we create a get request and after we get the response we assert the body

```Playwright
 test(`use request data`, async ({ request }) => {
        const newPost = await request
        .post(`https://wizard-world-api.herokuapp.com/Feedback`, {
            data: {
                "feedbackType": "General",
                "feedback": "string",
                "entityId": "3fa85f64-5717-4562-b3fc-2c963f66afa6"
            }
        })
        expect(newPost.ok()).toBeTruthy()
    })
```
In this example we create a post request  and assert if the request success