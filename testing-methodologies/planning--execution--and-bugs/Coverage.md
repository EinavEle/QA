# What is coverage?
Coverage means the area or percentage of a system that is covered by tests.
Coverage can be measured in code lines that are reached by the tests or by defining a test plan.
Usually, when designing test plans for features of a system, we can tell how well-covered is the specific feature we are testing.
The parts of our system that have no tests addressing them, are “uncovered”.
Most of the time, there is no real 100% coverage as it is almost always possible to think of more scenarios and more ways to challenge the system.
Having said that, we always try to cover as much as we can an be aware of areas that are “uncovered”
# Sanity
Sanity is the name of a test suite used to tell that the system is “basically functioning”.
Meaning it has low coverage of most areas of the system and it mostly covers the “happy path” tests.
We execute sanity tests pretty often since it should be a pretty small set of tests that can give us quick feedback.
# Regression
Regression testing is a software testing technique used to ensure that modifications or changes to a software system do not introduce new defects or cause unintended impacts on existing functionality. It involves retesting previously tested parts of the system to validate their continued correctness after changes have been made.
Every test that validates things that were implemented in the system in previous versions is considered part of the regression.
# Progression
Progression testing refers to testing of new functionality or features that are now being developed and are still not a working and functioning part of the system.
These are usually tested before being deployed to production and becoming a permanent part of application.
Once we have implemented regression tests and the features are released, these tests can also become a part of our regression suite.
