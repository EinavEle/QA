# Equivalence Partitioning
Equivalence partitioning is a technique used in software testing to group input data into different categories, where each category exhibits similar behavior. 
The main aim of equivalence partitioning is to minimize the number of test cases while still achieving thorough test coverage. 
By selecting representative test cases from each category, we can effectively validate the software. The underlying idea is that if one input within a category behaves correctly, then we can assume that all other inputs within the same category will also behave correctly. Equivalence partitioning streamlines the testing process, making it more efficient and reliable in identifying defects and ensuring the overall quality of software systems.
For example: if a certain function can accept only whole positive numbers but behaves differently for odd and even numbers, we can define these partitions:
- Odd whole numbers
- Even whole numbers
- Negative numbers, fractions, non numbers

We don’t have to test all the even numbers since they are all in the same partition.
# Boundary Tests
Boundary testing means testing the edges of the input range.
For example if a function should accept numbers between 18-90 we will test the following inputs:
- 17
- 18
- 90
- 91

This should provide coverage of all the different behaviors of this input.

# Decision Table Testing
Decision table testing is a software testing technique that involves creating a tabular representation of various combinations of inputs and corresponding actions or outcomes. It helps in systematically testing different scenarios and combinations of conditions and rules to ensure the correctness and effectiveness of a software system. By organizing inputs, conditions, and actions in a structured table format, decision table testing allows testers to easily identify all possible combinations and their expected results. This technique aids in comprehensive test coverage and assists in identifying any missing or redundant conditions or rules. Decision table testing enhances the overall quality and reliability of software by ensuring that all possible scenarios are considered and validated.

Let’s take for example a login page:
We have a user input and a password input.
We can make a decision table combining all the options relating to these inputs:
| Category | Rule 1  | Rule 2 | Rule 3 | Rule 4 |
|---------|----------|---------|---------|----|
|**Username** | F  | T | F | T |
|**Password** | F  | F | T | T |
|**Output** | E  | E | E | H |

Legend:
T - correct input
F - incorrect input
E - error
H - home page is shown

In the table above we have covered all the combinations of these two inputs and each of these combinations is one test case.
# State Transition Testing
State transition testing is a software testing technique that focuses on testing the behavior and transitions of a system as it moves between different states. It involves identifying the various states a system can be in and the events or actions that cause it to transition from one state to another. The primary objective of state transition testing is to ensure that the system responds correctly to different events and transitions smoothly between states as expected. Test cases are designed to cover different state transitions and validate the system's behavior during these transitions. By examining the system's response at each state change, testers can identify any potential issues or discrepancies in the system's behavior. State transition testing helps improve the reliability and robustness of software by thoroughly examining its behavior during state changes and ensuring that it operates correctly throughout its lifecycle.

For example, if we were to test an elevator system we could test the state transitions of an elevator, including initial state (idle on a floor), receiving a call from a floor, moving to the requested floor, opening/closing doors, accommodating passengers, moving between floors, and returning to the idle state.
# Use Case testing

Use case testing is a software testing technique that focuses on validating the functionality of a system based on its defined use cases. Use cases describe the interactions between actors (users, systems, or external entities) and the system, outlining the steps and conditions required to achieve a specific goal or desired outcome.
Most of the testers, most of the time, use this method since it is the clearest way to get from design to test.
A product manager defines the behavior of the system in a user story and the tester “translates” it into tests.

One very important term related to this type of testing is “Happy path”, happy path means the scenario where everything works as expected, without complicated edge cases or special behavior of the user.
In other words, the simple flows of the application that most users will use.
# Exploratory Testing

Exploratory testing is a dynamic and flexible software testing approach that emphasizes learning, discovery, and adaptation during the testing process. 
Unlike scripted testing, where test cases are predefined and followed step-by-step, exploratory testing involves simultaneous test design and execution. 
Testers explore the software system, investigate its behavior, and make real-time decisions on what to test, how to test it, and what areas to focus on.
