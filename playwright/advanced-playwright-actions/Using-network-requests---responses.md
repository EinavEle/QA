# Introduction
You can use network requests and responses to inspect and modify the communication between a web application and its backend server. 
This can be particularly useful for testing and automation scenarios, where you need to verify that the correct data is being sent and received by the application.

Playwright provides several features for working with network requests and responses. For example, you can:

- Intercept network requests and modify their behavior using route().
- Wait for specific network requests to complete using waitForRequest() and waitForResponse().
- Retrieve details about a network request or response using methods such as request.url(), request.method(), response.status(), and so on.
- Block or modify network requests and responses using setOfflineMode() or intercept().
- Simulate different network conditions such as slow connections and throttling using context.emulateNetworkConditions().

With these capabilities, you can simulate different network scenarios and validate the behavior of your application under different conditions.
 You can also modify network responses to test error handling or edge cases, and verify that your application is handling data correctly.

In summary, using network requests and responses in Playwright is an important part of testing and automating web applications, and can help you validate the behavior and performance of your application under different conditions.

# How to wait for request/response
```Playwright
 test(`How to wait for request/response`, async ({ page }) => {
        const responsePromise = page.waitForResponse('https://www.google.com')
        await page.goto('https://www.google.com')
        const response = await responsePromise
        expect(response.status()).toBe(200)
    })
```

In this example, we navigate to a webpage using page.goto(). 
Then, we use page.waitForResponse() to wait for a network response that matches a specific condition, in this case a URL that includes 'https://www.google.com'.
Once the response is received, we can retrieve the status code using response.status() and assert it.

Note that page.waitForResponse() can also accept other conditions such as a specific status code or response headers. You can use this function to wait for network requests and responses that are important for your testing or automation scenarios.
