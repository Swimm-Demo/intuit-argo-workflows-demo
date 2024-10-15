---
title: Initializing and Managing Argo Workflows CLI Commands
---
This document will cover the process of initializing and managing Argo Workflows CLI commands, which includes:

1. Setting up the main command structure
2. Registering subcommands
3. Configuring specific commands for different functionalities.

Technical document: <SwmLink doc-title="Initializing and Managing Argo Workflows CLI Commands">[Initializing and Managing Argo Workflows CLI Commands](/.swm/initializing-and-managing-argo-workflows-cli-commands.fiofzic9.sw.md)</SwmLink>

# [Setting up the main command structure](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v/docs/fiofzic9#newcommand-initialization)

The main command structure is the foundation of the Argo Workflows CLI. It sets up the basic usage information and different modes of operation. This structure provides users with a comprehensive interface to interact with Argo Workflows. The main command includes details on how to use the CLI in various modes, such as Kubernetes API Mode, Argo Server GRPC Mode, and Argo Server HTTP1 Mode. Each mode offers different capabilities and is suited for specific use cases, ensuring flexibility for the end user.

# [Registering subcommands](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v/docs/fiofzic9#subcommand-registration)

Subcommands extend the functionality of the CLI, allowing users to perform specific actions like managing workflows, templates, and archives. Each subcommand is designed to handle a particular task, making the CLI versatile and capable of managing a wide range of operations. For example, subcommands like `NewDeleteCommand` and `NewGetCommand` enable users to delete workflows and retrieve workflow details, respectively. This modular approach ensures that the CLI can be easily extended to include new functionalities as needed.

# [Configuring specific commands for different functionalities](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v/docs/fiofzic9#newcronworkflowcommand)

Specific commands are configured to handle particular functionalities within the CLI. For instance, the `NewCronWorkflowCommand` is set up to manage cron workflows. This command includes subcommands for getting, listing, creating, deleting, linting, suspending, resuming, and updating cron workflows. This is essential for users who need to automate workflows on a scheduled basis, providing them with the tools to manage and monitor these workflows effectively.

The `NewServerCommand` initializes the Argo Server, which handles API requests and serves the Argo UI. This command configures various server settings such as authentication modes, TLS, namespaces, and more. Setting up the server environment is critical for managing and executing workflows, ensuring that users have a reliable and secure platform to run their workflows.

The `NewTemplateCommand` is designed for manipulating workflow templates. It includes subcommands for getting, listing, creating, deleting, linting, and updating workflow templates. This command is vital for users who need to manage reusable workflow templates efficiently, allowing them to streamline their workflow creation process.

The `NewClusterTemplateCommand` focuses on cluster-wide templates. It includes subcommands similar to the `NewTemplateCommand` but is intended for managing templates across multiple namespaces. This is essential for users who need to deploy and manage workflows at a cluster level, ensuring consistency and efficiency across different environments.

The `NewArchiveCommand` manages the workflow archive. It includes subcommands for listing, getting, deleting, and resubmitting archived workflows. This command is crucial for users who need to interact with archived workflows, providing them with the tools to manage and retrieve historical workflow data.

The `NewRetryCommand` allows users to retry one or more workflows. It supports options for retrying workflows by UID, label selector, or field selector. This command is important for users who need to re-execute workflows that may have failed or require reprocessing, ensuring that workflows can be retried with ease.

The `NewResubmitCommand` enables users to resubmit one or more workflows. Similar to the retry command, it supports resubmission by UID, label selector, or field selector. Additional options include setting workflow priority and reusing successful steps from previous runs. This command is essential for workflows that need to be rerun with potentially different parameters or configurations.

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
