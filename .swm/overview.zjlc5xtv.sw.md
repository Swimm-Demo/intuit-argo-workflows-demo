---
title: Overview
---
The repository 'intuit-argo-workflows-demo' is focused on Argo Workflows, an open-source container-native workflow engine for orchestrating parallel jobs on Kubernetes. It allows users to define workflows where each step is a container and supports modeling multi-step workflows as a sequence of tasks or using a directed acyclic graph (DAG).

## Main Components

### API Clients

- **Client**
  - **Clientset**
    - <SwmLink doc-title="Clientset in Argo Workflows">[Clientset in Argo Workflows](/.swm/clientset-in-argo-workflows.e22hslk3.sw.md)</SwmLink>
  - **Listers**
    - <SwmLink doc-title="Introduction to Workflow Listers">[Introduction to Workflow Listers](/.swm/introduction-to-workflow-listers.75302rp5.sw.md)</SwmLink>
  - **Informers**
    - <SwmLink doc-title="Informers in Client">[Informers in Client](/.swm/informers-in-client.akdlpaqw.sw.md)</SwmLink>
- **Apiclient**
  - **Workflowarchive**
    - <SwmLink doc-title="Workflow Archive Overview">[Workflow Archive Overview](/.swm/workflow-archive-overview.hs5zqewf.sw.md)</SwmLink>
  - **Workflow**
    - <SwmLink doc-title="Understanding Workflow Management">[Understanding Workflow Management](/.swm/understanding-workflow-management.9ptcgl9q.sw.md)</SwmLink>
    - **Flows**
      - <SwmLink doc-title="Registering a Workflow Service Handler">[Registering a Workflow Service Handler](/.swm/registering-a-workflow-service-handler.yj0nvb28.sw.md)</SwmLink>
  - **Sensor**
    - <SwmLink doc-title="Basic Concepts of Sensor Operations">[Basic Concepts of Sensor Operations](/.swm/basic-concepts-of-sensor-operations.8tzkf7e4.sw.md)</SwmLink>
  - **Info**
    - <SwmLink doc-title="Getting Started with Info Service">[Getting Started with Info Service](/.swm/getting-started-with-info-service.y0isv6kb.sw.md)</SwmLink>
  - **Cronworkflow**
    - <SwmLink doc-title="Introduction to CronWorkflow Management">[Introduction to CronWorkflow Management](/.swm/introduction-to-cronworkflow-management.oc0m5el6.sw.md)</SwmLink>
  - **Clusterworkflowtemplate**
    - <SwmLink doc-title="Getting Started with ClusterWorkflowTemplate in Apiclient">[Getting Started with ClusterWorkflowTemplate in Apiclient](/.swm/getting-started-with-clusterworkflowtemplate-in-apiclient.1qvzltpk.sw.md)</SwmLink>
  - **Workflowtemplate**
    - <SwmLink doc-title="Introduction to Workflow Template Management">[Introduction to Workflow Template Management](/.swm/introduction-to-workflow-template-management.2z9pb3kp.sw.md)</SwmLink>
  - **Http1**
    - <SwmLink doc-title="Introduction to Http1 Client">[Introduction to Http1 Client](/.swm/introduction-to-http1-client.29a6by2d.sw.md)</SwmLink>
    - **Flows**
      - <SwmLink doc-title="Creating a Server Dry Run">[Creating a Server Dry Run](/.swm/creating-a-server-dry-run.7xpgfnvz.sw.md)</SwmLink>
      - <SwmLink doc-title="Creating a Workflow">[Creating a Workflow](/.swm/creating-a-workflow.8un6nlga.sw.md)</SwmLink>
  - **Eventsource**
    - <SwmLink doc-title="Exploring Eventsource in Apiclient">[Exploring Eventsource in Apiclient](/.swm/exploring-eventsource-in-apiclient.uauffvt0.sw.md)</SwmLink>
  - **Flows**
    - <SwmLink doc-title="Workflow Validation Process">[Workflow Validation Process](/.swm/workflow-validation-process.shucexos.sw.md)</SwmLink>
    - <SwmLink doc-title="Client Creation and Configuration Flow">[Client Creation and Configuration Flow](/.swm/client-creation-and-configuration-flow.mgf01p1z.sw.md)</SwmLink>
    - <SwmLink doc-title="Creating and Configuring an API Client">[Creating and Configuring an API Client](/.swm/creating-and-configuring-an-api-client.zgqh4kmv.sw.md)</SwmLink>
- **Apis**
  - **Zz generated deepcopy**
    - <SwmLink doc-title="Exploring Generated DeepCopy Functions">[Exploring Generated DeepCopy Functions](/.swm/exploring-generated-deepcopy-functions.ats4ioag.sw.md)</SwmLink>
  - **Workflow types**
    - <SwmLink doc-title="Introduction to Workflow Types">[Introduction to Workflow Types](/.swm/introduction-to-workflow-types.6djl3s5b.sw.md)</SwmLink>
    - **Flows**
      - <SwmLink doc-title="Retrieving and Relocating an Artifact">[Retrieving and Relocating an Artifact](/.swm/retrieving-and-relocating-an-artifact.nv7up0rb.sw.md)</SwmLink>

### User Interface

The User Interface (UI) is the visual component of the application that allows users to interact with the system. It includes elements like forms, buttons, and displays that facilitate user input and provide feedback. The UI is designed to be intuitive and user-friendly, ensuring that users can easily navigate and perform tasks within the application.

- <SwmLink doc-title="User Interface Overview">[User Interface Overview](/.swm/user-interface-overview.yfmnnm37.sw.md)</SwmLink>
- **Shared**
  - <SwmLink doc-title="Overview of the Shared Directory">[Overview of the Shared Directory](/.swm/overview-of-the-shared-directory.2ybpk4sp.sw.md)</SwmLink>
  - **Services**
    - <SwmLink doc-title="Overview of Shared Services">[Overview of Shared Services](/.swm/overview-of-shared-services.l9ebuux5.sw.md)</SwmLink>
  - **Components**
    - <SwmLink doc-title="Exploring Shared Components">[Exploring Shared Components](/.swm/exploring-shared-components.wtmn9421.sw.md)</SwmLink>
  - **Flows**
    - <SwmLink doc-title="Rendering and Managing Workflows">[Rendering and Managing Workflows](/.swm/rendering-and-managing-workflows.9mzygm1o.sw.md)</SwmLink>
- **Workflows**
  - <SwmLink doc-title="Basic Concepts of Workflows in UI">[Basic Concepts of Workflows in UI](/.swm/basic-concepts-of-workflows-in-ui.bejo9d1s.sw.md)</SwmLink>
  - **Flows**
    - <SwmLink doc-title="Rendering and Managing Workflow Details">[Rendering and Managing Workflow Details](/.swm/rendering-and-managing-workflow-details.snxj1izv.sw.md)</SwmLink>
- **Flows**
  - <SwmLink doc-title="EventFlowPage Initialization and Management">[EventFlowPage Initialization and Management](/.swm/eventflowpage-initialization-and-management.k9p50ps8.sw.md)</SwmLink>

### Flows

- <SwmLink doc-title="Executing Steps in a Workflow">[Executing Steps in a Workflow](/.swm/executing-steps-in-a-workflow.xh09i7a6.sw.md)</SwmLink>
- <SwmLink doc-title="Initializing and Managing Argo Workflows CLI Commands">[Initializing and Managing Argo Workflows CLI Commands](/.swm/initializing-and-managing-argo-workflows-cli-commands.fiofzic9.sw.md)</SwmLink>
- <SwmLink doc-title="Setting Up and Running the Argo Server">[Setting Up and Running the Argo Server](/.swm/setting-up-and-running-the-argo-server.2skz0ne7.sw.md)</SwmLink>
- <SwmLink doc-title="Retrieving Artifact Files Flow">[Retrieving Artifact Files Flow](/.swm/retrieving-artifact-files-flow.sk2kkibv.sw.md)</SwmLink>
- <SwmLink doc-title="Retrying a Workflow">[Retrying a Workflow](/.swm/retrying-a-workflow.ij7i4fc0.sw.md)</SwmLink>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
