# Functional
**Different levels of code access**
When performing functional tests, we can have different levels of access or involvement with the application code, which will affect our way of testing.

**Black Box Testing**

Black Box Testing is a type of software testing where testers evaluate a software application's functionality without knowing its internal workings or code.
In other words, testers treat the software as a "black box" and focus on inputting data and verifying the output without any knowledge of how the system processes the data. 
Black Box Testing is useful in identifying defects and bugs that could affect the software's usability and functionality.
For example the tester would enter valid and invalid login credentials and verify if the application behaves as expected, such as granting access to authorized users and denying access to unauthorized users. 
The tester doesn't need to know how the application verifies user credentials or how the system is implemented. Instead, they focus on the inputs, outputs, and the system's behavior.

**White Box Testing**

White Box Testing is a type of software testing where testers evaluate the internal workings or code of a software application. 
Testers have access to the software's code and use it to design test cases that verify the software's functionality and logic. 
White Box Testing is useful in identifying defects and bugs that could affect the software's performance and stability, as well as ensuring that the code meets industry standards and best practices.
For example the tester would have access to the algorithm's code and use it to design test cases that cover different scenarios, such as sorting a small array, a large array, and an array with duplicate values. The tester would then execute the tests and verify that the output is correct and matches the expected result. 
The tester needs to understand how the algorithm works, its code, and its internal logic to design effective test cases.

**Gray Box Testing**

Gray Box Testing is a type of software testing where testers have partial knowledge of the internal workings or code of a software application. 
Testers have limited access to the software's code, database, or design documents, but not the full information. 
Gray Box Testing is useful in identifying defects and bugs that could affect the software's functionality and performance, as well as ensuring that the software meets user requirements.
For example the tester would use the design documents to understand how the application's login feature works, and then design test cases to verify its functionality, such as testing the login process with valid and invalid credentials, and testing what happens when the user forgets their password. 
The tester has limited knowledge of the code, but enough information to design effective test cases and identify defects that could affect the application's usability and functionality.

**Performance/Load/stress**
- Performance testing is about testing how long it takes a single action to be performed. For example how long it takes for one user to login to the system.
- Load testing means testing the system under bigger amounts of data. Like performing functionality tests on our system but with 10x the amount of data we usually test with. This is sometimes done incrementally so we can see what is the amount of data that makes specific tests fail.
- Stress testing means putting the system under high concurrent usage. It can mean many users or many actions by a few users. In stress testing we test the timing and success rates of our actions. For example, 100 users call the server attempting to get some information. The results will show us how long one call took, what is the average, the median, the minimum time, the maximum time, and the success rate of these calls.

**Usability**
- Usability testing is about making sure that software is easy to use and user-friendly.
- It involves testing the interface and user experience to ensure that users can navigate the software without difficulty.
- Usability testing can be done through various methods, such as having users perform tasks while being observed or filling out surveys.
- Usability testing can help identify areas of improvement in the software's design and functionality, making it more appealing to users.
- The goal of usability testing is to ensure that users can perform tasks efficiently and effectively, without frustration or confusion.
- Usability testing is especially important in industries such as e-commerce, where a poor user experience can lead to lost sales and a negative reputation.

**Security**
- Security testing is a type of software testing that focuses on ensuring that software systems are secure from external threats.
- The goal of security testing is to identify vulnerabilities, risks and threats to the software application, and to ensure that it can withstand attacks from hackers and malicious users.
- Security testing involves simulating attacks on the system and testing its ability to prevent unauthorized access, protect sensitive data, and maintain the integrity of the system.
- There are various types of security tests that can be performed, including penetration testing, vulnerability scanning, and risk assessment.
- Security testing is crucial for applications that handle sensitive information, such as financial and healthcare systems, to ensure that confidential information is protected.
- By identifying and addressing security flaws in software, security testing helps to prevent cyber attacks and data breaches, safeguarding the reputation of the company and the privacy of its users.

**Compatibility**
- Compatibility testing is a type of software testing that ensures that the software works correctly across different platforms, devices, browsers, and operating systems.
- The goal of compatibility testing is to ensure that the software functions as expected regardless of the environment it is running on.
- Compatibility testing involves testing the software on a range of devices and operating systems to ensure that it is compatible with all of them and works smoothly.
- It also involves testing the software with different browsers and versions to ensure that it displays properly and all functionalities work as expected.
- Compatibility testing helps identify compatibility issues, such as software crashes or display errors, which may arise due to differences in platforms and configurations.
- The importance of compatibility testing has increased in recent years due to the wide variety of devices, browsers, and platforms that users may use to access the software.
- By conducting compatibility testing, software developers can ensure that their software works consistently across different platforms and devices, ensuring a better user experience for their customers.

**Localization**

Localization testing means testing the system for support of different languages.
It can include testing translations, design (left to right, etc..), converting units (kilos to pounds, kilometers to miles, etc..), and more.
