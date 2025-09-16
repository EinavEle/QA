# Running tests in loop
In Playwright, it's possible to run tests in a loop by parameterizing them with different input values. 
This can be useful for testing a function or a component with different scenarios and inputs.

Parameterizing a test involves defining a set of input values and running the test multiple times with each input value.
The output of the test is then verified against the expected results for each input value.

For example, suppose you have a function that adds two numbers and returns the result. You can parameterize the test for this function by providing a set of input values, 
such as (1, 2), (3, 4), and (5, 6). The test would then run three times with each input value, and the output would be verified against the expected result.

Here's an example of how you can parameterize a test in Playwright:

```Playwright
import { test, expect } from '@playwright/test';

test.describe('Addition function', () => {
    const testData = [
        { a: 1, b: 2, expected: 3 },
        { a: 3, b: 4, expected: 7 },
        { a: 5, b: 6, expected: 11 },
    ];

    testData.forEach(({ a, b, expected }) => {
        test(`Adding ${a} and ${b} should return ${expected}`, async () => {
            const result = await add(a, b);
            expect(result).toBe(expected);
        });
    });
});

async function add(a, b) {
    return a + b
}
```

In this example, the testData array contains three sets of input values, and the forEach loop runs the test for each set of input values. The add function is called with the input values, and the result is verified against the expected output using the expect function.
