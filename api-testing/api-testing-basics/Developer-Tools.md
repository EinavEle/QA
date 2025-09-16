# *What is “developer tools”?*
"Developer tools" is a set of tools that allow developers to inspect and manipulate the code of a website. 
They're built into most modern web browsers like Chrome, Firefox, and Edge. With these tools, developers can debug JavaScript code, monitor network activity, analyze web page performance, test accessibility, and more. 
They're really useful for web developers and designers to troubleshoot and optimize their code, as well as to test and debug their websites and web applications.
# *How to use it?*
**Step 1: Open the Developer Tools**
- Open Chrome browser and navigate to the webpage where the REST API request is being made.
- Right-click anywhere on the page and select "Inspect" from the context menu or you can click the “F12” key.
- This will open the Developer Tools in Chrome.

**Step 2: Go to the Network Tab**
- In the Developer Tools window, click on the "Network" tab.
- This will display a list of all the network requests made by the webpage.

**Step 3: Trigger the REST API Request**
- In order to see the REST API request, you need to trigger it by performing the action that would make the request.
- For example, if the REST API is used to load data from a server, you need to perform the action that loads the data.

**Step 4: View the REST API Request**
- Once the REST API request is triggered, you should see it in the list of network requests in the Network tab.
- The REST API request will be shown as a row in the list, with details such as the request method (GET, POST, etc.), the URL, the status code, and the response.

**Step 5: Inspect the Request Details**
- You can click on the row of the REST API request to see more details about it, such as the request and response headers, the request payload (if any), and the response data.

**Example:**
Let's say you want to see the REST API request that is made when you search for something on Google.
Here's how you can do it:
- Open Google in Chrome.
- Open the Developer Tools by right-clicking anywhere on the page and selecting "Inspect".
- Go to the "Network" tab.
- Type a search query in the Google search bar and hit Enter.
- You should see a new row in the list of network requests in the Network tab, labeled "https://www.google.com/search?q=your+search+query".
- Click on this row to see more details about the REST API request, such as the headers, payload, and response data.