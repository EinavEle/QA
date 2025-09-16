# How to install and run our first app via Appium?
Step 1: Install Node.js

- Visit the official Node.js website (https://nodejs.org).
- Download the latest stable version of Node.js for your operating system (Windows, macOS, or Linux).
- Run the installer and follow the on-screen instructions to complete the installation.

Step 2: Install Appium Server

- Open a command prompt or terminal window.
- Run the following command to install Appium globally:
- `npm install -g appium`
This command will install the Appium server on your system.

Step 3: Start Appium Server

- Open a command prompt or terminal window.
- Run the following command to start the Appium server:

`npx appium`
By default, Appium starts listening on ‘localhost:4723’.

Step 4 : Install Appium Inspector

- Appium Inspector is part of the Appium Desktop application, which provides a graphical user interface for interacting with Appium.
- Visit the Appium Desktop GitHub repository (https://github.com/appium/appium-desktop) and download the latest version of Appium Desktop for your operating system.
- Once downloaded, install Appium Desktop by running the installer.
- After the installation is complete, launch the Appium Desktop application.

Step 5: adding environment variables
Run the following command on terminal:
```terminal
export /Users/<YouAreName>/Library/Android/sdk/platform-tools
export /Users/<YouAreName>/Library/Android/sdk/tools
export /Users/<YouAreName>/Library/Android/sdk/tools/bin
export /Users/<YouAreName>/Library/Android/sdk/emulator
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-17.jdk/Contents/Home
export PATH=$PATH:/Users/<YouAreName>/Library/Android/sdk/tools/bin
```
For Windows follow the next link:
https://docs.oracle.com/en/database/oracle/machine-learning/oml4r/1.5.1/oread/creating-and-modifying-environment-variables-on-windows.html#GUID-DD6F9982-60D5-48F6-8270-A27EC53807D0
