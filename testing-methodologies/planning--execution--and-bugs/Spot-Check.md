Write a bug when the system allows sending an empty form even though an error message should pop up.
<details>
  <summary>
    Solution
  </summary>

1. Bug Title: Error message not displayed when submitting an empty form
2. Bug Description:
3. Steps to Reproduce:
a) Navigate to the registration page.
b) Leave all fields blank.
c) Click on the "Submit" button.
4. Expected Behavior:
An error message should be displayed indicating that the required fields are missing.
5. Actual Behavior:
After clicking on the "Submit" button, the form is submitted without any validation, and no error message is displayed.
6. Environment:
**Operating System: Windows 10
Browser: Google Chrome, version 89.0.4389.82**
7. Additional Information:
- This issue occurs consistently on both desktop and mobile devices.
- The form includes the following required fields: Name, Email, and Password.
- Other form fields without the required attribute are not affected.
- The form validation JavaScript function is implemented and should trigger an error message when required fields are empty.
- The error message element is present in the HTML markup but remains hidden even when the form is submitted with empty fields.
8. Severity: Medium
9. Impact:
- Users are able to submit incomplete registration forms, leading to incomplete or invalid data being stored in the system.
- Lack of validation feedback can result in user frustration and confusion.
- This issue can negatively impact data integrity and the user experience.
10. Expected Fix:
a) Update the form validation logic to properly check for empty required fields.
b) Display the error message element and show the appropriate error message when required fields are empty.
c) Ensure that the error message is clearly visible to users and provides guidance on the missing fields.
11. Attachments:
- Screenshots of the registration form before and after submitting an empty form.
- Relevant sections of the HTML markup and JavaScript code related to form validation.


</details>