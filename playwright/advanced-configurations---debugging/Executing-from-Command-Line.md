To execute Playwright tests from the command line, you can use the npx playwright test command. 

Here are the basic steps:

1. Open your terminal or command prompt.
2. Navigate to the directory that contains your Playwright test files.
3. Run the following command: ```npx playwright test```

This will execute all the Playwright tests in the current directory using the default test runner.

You can also pass command-line options to the npx playwright test command. Here are a few examples:

- To run a specific test file, pass the path to the test file:

```npx playwright test path/to/test/file.ts```

- To run a specific test case in a file, use the --test option followed by the test name or part of the test name:

```npx playwright test --test "Test case name"```

- To run only tests that match a specific string, use the --grep option followed by the string:

```npx playwright test --grep "string to match"```

- To run tests with a specific tag, use the --grep option followed by the tag name:

```npx playwright test --grep @tagName```
