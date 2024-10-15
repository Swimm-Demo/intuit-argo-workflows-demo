---
title: Creating a Server Dry Run
---
This document will cover the process of creating a server dry run, which includes:

1. Initiating the dry run request
2. Handling the server response
3. Validating the workflow configuration.

Technical document: <SwmLink doc-title="Creating a Server Dry Run">[Creating a Server Dry Run](/.swm/creating-a-server-dry-run.7xpgfnvz.sw.md)</SwmLink>

# [Initiating the Dry Run Request](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v/docs/7xpgfnvz#createserverdryrun)

The process begins with initiating a dry run request to the server. This involves sending a request to the server with a 'dryRun' parameter. The purpose of this step is to simulate the creation of a workflow without actually committing it. This allows users to validate their workflow configuration before making any real changes. The request includes all necessary workflow data and specifies that it is a dry run, ensuring that the server processes it accordingly without making permanent changes.

# [Handling the Server Response](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v/docs/7xpgfnvz#do)

Once the server receives the dry run request, it processes the workflow data and returns a response. The response is then handled to check for any errors and to decode the output if necessary. This step is crucial as it ensures that any issues with the workflow configuration are identified and communicated back to the user. The server's response provides a representation of what the workflow would look like if it were actually created, allowing users to review and make any necessary adjustments.

# [Validating the Workflow Configuration](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v/docs/7xpgfnvz#flatten)

The final step involves validating the workflow configuration based on the server's response. This step ensures that the workflow is correctly configured and ready for actual creation. The validation process includes checking the workflow's structure, parameters, and any other relevant details. By performing this validation, users can be confident that their workflow will function as expected when it is eventually created. This step helps prevent errors and ensures a smooth workflow creation process.

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
