Cucumber is an open-source tool for implementing BDD in software development. It uses Gherkin, a human-readable language, to describe system behavior from various perspectives.

Cucumber has three main parts:
- Feature Files: Written in Gherkin, they describe the expected system behavior and contain scenarios made up of steps that detail specific user stories or test cases.
- Step Definitions: The code that corresponds to the steps described in feature files. Step definitions are written in programming languages such as Java or Ruby and are bound to feature files' steps through regular expressions or other matching mechanisms.
- Test Runner: Executes feature files and step definitions and reports results. Cucumber supports test runners like JUnit or TestNG in Java and RSpec in Ruby.

To bind steps to Gherkin, step definitions in code correspond to the feature files' steps. Cucumber matches steps in feature files to step definitions using regular expressions or other mechanisms and executes the code when each step is encountered during testing.