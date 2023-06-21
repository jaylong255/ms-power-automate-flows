# OneDrive Watcher
The following is a draft for a project plan to watch a one drive folder for new files, send an email notification to a given email list, then move the files to another folder.

## Bot Consultation
I spent a few minutes imagining what a solution might generally entail like based off of my own personal experience and a quick glance at the MS Power Automate Flow documentation. Then I wrote a prompt to get an opinion from GPT-4. Here is that initial consultation:

### Prompt
write me a project plan for developing a microsoft power automate flow that watches a one drive folder, sends an email notification to a given email list, then moves the file to another folder. include what languages you would choose from to script the automation, the process of setting up the flow itself, options for how you would handle authentication, options for how you would manage queuing for when the initial folder was updated mulitple times in a short period of time. include examples of specific code snippets from the script. explain how you would deploy changes to the script using github actions workflows. then make a list of other possible issues and concerns you can predict that were not mentioned above.

### Response
Project Plan: Developing a Microsoft Power Automate Flow

1. Project Overview:
   - Objective: Develop a Microsoft Power Automate flow that monitors a OneDrive folder, sends email notifications to a given email list, and moves the files to another folder.
   - Languages: The automation can be scripted using either Power Automate's built-in actions and expressions or custom code snippets in languages such as JavaScript, C#, or PowerShell.

2. Setting up the Flow:
   - Sign in to Microsoft Power Automate (flow.microsoft.com) using your Microsoft account.
   - Create a new flow and provide a suitable name for it.
   - Choose a trigger action: "When a file is created or modified (properties only)" for the OneDrive connector.
   - Configure the trigger by specifying the OneDrive folder to monitor.
   - Add an action to send an email notification, providing the email subject, recipient list, and email body.
   - Add an action to move the file to the desired folder using the "Move file" action from the OneDrive connector.
   - Configure the action by specifying the source and destination folders.
   - Save the flow.

3. Authentication Options:
   - Power Automate provides authentication options for different services, such as OneDrive. The most common options include:
     a. Using the account associated with the Power Automate flow.
     b. Using a dedicated service account with appropriate permissions.
     c. Configuring OAuth or API keys for authentication if required by the service.

4. Managing Queuing:
   - When the initial folder is updated multiple times in a short period, you can handle queuing by using a combination of the "Do Until" and "Delay" actions.
   - Within the "Do Until" action, you can add a condition to check if the folder is no longer being modified. If it is still being modified, add a "Delay" action to wait for a specific period and then check again.

5. Code Snippets:
   - PowerShell: Move-Item -Path "sourcePath" -Destination "destinationPath"
   - JavaScript (using Power Automate expression): outputs('Create_file')?['body']?['{Path}']
   - C# (using Power Automate expression): triggerOutputs()['body/{Path}']

6. Deploying Changes with GitHub Actions Workflows:
   - Set up a GitHub repository to store your Power Automate flow.
   - Create a new GitHub Actions workflow to automate the deployment process.
   - Configure the workflow to trigger when changes are pushed to the repository.
   - Use the GitHub Actions API or PowerShell scripting to call the Power Automate API and update the flow definition.
   - You can leverage the Power Automate Management Connector or PowerShell cmdlets like `Update-FlowDefinition`.

7. Other Possible Issues and Concerns:
   - Handling file name conflicts during the move operation.
   - Implementing error handling and notifications for any failures in the flow.
   - Dealing with file size limitations or restrictions imposed by OneDrive or email providers.
   - Ensuring proper access and permissions for the Power Automate flow and associated services.
   - Managing potential delays in email delivery or potential issues with the email server.
   - Considering data privacy and security aspects, especially when dealing with sensitive files or email content.
   - Ensuring proper error logging and monitoring to track flow execution and diagnose issues.
   - Testing the flow thoroughly to handle various scenarios, including edge cases and error handling.