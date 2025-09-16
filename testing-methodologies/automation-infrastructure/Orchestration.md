# Intro
Orchestration in automation testing is all about managing and coordinating different parts of the testing process. 
It involves organizing and sequencing tests, handling dependencies, and controlling the overall testing workflow.

With orchestration, you can execute tests in a controlled and systematic way. It helps streamline testing, improve efficiency, and ensure consistency. 
By orchestrating tests, you can handle complex scenarios, manage dependencies between tests, and achieve thorough test coverage.
# Don’t make your framework do the build server’s job!
Avoid burdening your automation framework with tasks that should be handled by the build server. 
The build server has its own responsibilities, like managing builds, running tests, and deploying applications.

Instead of duplicating the build server's work, integrate your automation tests into the existing build pipeline. 
This way, each component can focus on its specific tasks, resulting in a more efficient workflow.

By utilizing the build server for tasks such as triggering test execution, managing test environments, and generating reports, you can benefit from its built-in features and scalability. 
This approach keeps your automation framework lightweight, focused on test implementation, and avoids unnecessary complexity.
# Config 
The framework should allow for external configuration using environment variables or a config file. This way, you can easily adjust the settings without modifying the framework's code.

When using a build server, it can inject the necessary configuration during the build process. 
This ensures that the configuration is set correctly before running the tests. 
The build server can provide environment-specific details like URLs, credentials, or API keys based on the target environment.

Separating configuration from the framework code makes it easier to manage and update the settings as needed. 
It also allows for seamless integration with different environments, enabling smoother deployment and test execution.

By supporting external configuration and leveraging the build server's capabilities, you create a more flexible and scalable automation framework.
# Credentials 
Credentials should never be hardcoded in your automation framework code. Instead, they should be supplied during the build process to ensure security and flexibility.

Hard Coding credentials in the code poses a security risk as it can be accessed by multiple users or stored in version control systems, potentially leading to unauthorized access.

To handle credentials securely, provide them externally during the build process. This can be done using environment variables, configuration files, or secret management systems. The build server can inject the appropriate credentials based on the target environment or user-specific configurations.

By separating credentials from the code and supplying them during the build process, you maintain better security and allow for easier management and rotation of credentials without modifying the code itself.
# Parameters
In automation testing, parameters are customizable values or options that can be passed via the command line during test execution. 
They allow you to tailor the test run without modifying the code or configurations directly. Here are some examples of injectable parameters:

- Tags: Categorize and selectively run tests based on specific criteria.
- Environment: Easily switch between different test environments.
- Output Folder: Configure the location for storing test reports and logs.
- Custom Parameters: Define additional values like timeouts or data sources for specific tests.

Injecting parameters via the command line provides flexibility and customization options for your automation framework without the need for code changes. 
It empowers testers and developers to adapt the test execution process to different scenarios or preferences.


Simply put, automation frameworks are responsible for creating and managing tests, while build servers handle the execution and orchestration of those tests. This separation allows frameworks to focus on test development.
