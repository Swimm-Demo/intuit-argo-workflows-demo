---
title: Introduction to CronWorkflow Management
---
# Introduction to <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="17:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow cronWorkflow = 2;">`CronWorkflow`</SwmToken> Management

<SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="17:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow cronWorkflow = 2;">`CronWorkflow`</SwmToken> is the definition of a scheduled workflow resource. It is designed to wrap a `workflowSpec` and mimic the options of Kubernetes CronJobs. In essence, <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="17:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow cronWorkflow = 2;">`CronWorkflow`</SwmToken> is a Workflow with some specific cron options.

# Managing <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="17:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow cronWorkflow = 2;">`CronWorkflow`</SwmToken>

The Apiclient package provides various methods to manage CronWorkflows, including creating, listing, updating, and deleting them. It also includes methods for suspending and resuming CronWorkflows.

You can create CronWorkflows with the CLI using the <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="2:13:13" line-data="option go_package = &quot;github.com/argoproj/argo-workflows/pkg/apiclient/cronworkflow&quot;;">`argo`</SwmToken>` `<SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="61:11:11" line-data="      post : &quot;/api/v1/cron-workflows/{namespace}/lint&quot;">`cron`</SwmToken>` create` command, specifying the configuration file. For example, <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="2:13:13" line-data="option go_package = &quot;github.com/argoproj/argo-workflows/pkg/apiclient/cronworkflow&quot;;">`argo`</SwmToken>` `<SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="61:11:11" line-data="      post : &quot;/api/v1/cron-workflows/{namespace}/lint&quot;">`cron`</SwmToken>` create cron.yaml` will create a <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="17:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow cronWorkflow = 2;">`CronWorkflow`</SwmToken> based on the settings in `cron.yaml`.

You can list existing CronWorkflows with <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="2:13:13" line-data="option go_package = &quot;github.com/argoproj/argo-workflows/pkg/apiclient/cronworkflow&quot;;">`argo`</SwmToken>` `<SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="61:11:11" line-data="      post : &quot;/api/v1/cron-workflows/{namespace}/lint&quot;">`cron`</SwmToken>` list` to see their status and schedules.

# <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="17:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow cronWorkflow = 2;">`CronWorkflow`</SwmToken> Spec

The <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="17:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow cronWorkflow = 2;">`CronWorkflow`</SwmToken> spec includes the `workflowSpec` and `workflowMetadata`, along with specific cron options such as schedule, concurrency policy, and starting deadline seconds. These options allow you to fine-tune the behavior of your scheduled workflows.

# Main Functions

There are several main functions in <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="17:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow cronWorkflow = 2;">`CronWorkflow`</SwmToken>. Some of them are creating, listing, updating, and deleting. We will dive a little into creating and listing.

## Creating CronWorkflows

The `CronWorkflows` can be created using the CLI with the command <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="2:13:13" line-data="option go_package = &quot;github.com/argoproj/argo-workflows/pkg/apiclient/cronworkflow&quot;;">`argo`</SwmToken>` `<SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="61:11:11" line-data="      post : &quot;/api/v1/cron-workflows/{namespace}/lint&quot;">`cron`</SwmToken>` create cron.yaml`. This command schedules the workflow according to the specified cron schedule.

## Listing CronWorkflows

The `CronWorkflows` can be listed using the CLI with the command <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="2:13:13" line-data="option go_package = &quot;github.com/argoproj/argo-workflows/pkg/apiclient/cronworkflow&quot;;">`argo`</SwmToken>` `<SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="61:11:11" line-data="      post : &quot;/api/v1/cron-workflows/{namespace}/lint&quot;">`cron`</SwmToken>` list`. This command displays all the scheduled workflows along with their status and schedule.

# <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="17:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow cronWorkflow = 2;">`CronWorkflow`</SwmToken> Endpoints

<SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="17:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow cronWorkflow = 2;">`CronWorkflow`</SwmToken> Endpoints provide programmatic access to manage CronWorkflows.

## <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="65:3:3" line-data="  rpc CreateCronWorkflow(CreateCronWorkflowRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow) {">`CreateCronWorkflow`</SwmToken>

The <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="65:3:3" line-data="  rpc CreateCronWorkflow(CreateCronWorkflowRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow) {">`CreateCronWorkflow`</SwmToken> endpoint allows clients to create a new <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="17:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow cronWorkflow = 2;">`CronWorkflow`</SwmToken>. It accepts a <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="15:2:2" line-data="message CreateCronWorkflowRequest {">`CreateCronWorkflowRequest`</SwmToken> message containing the namespace, the <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="17:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow cronWorkflow = 2;">`CronWorkflow`</SwmToken> definition, and creation options. The corresponding HTTP method is POST, and the URL pattern is <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="61:6:17" line-data="      post : &quot;/api/v1/cron-workflows/{namespace}/lint&quot;">`/api/v1/cron-workflows/{namespace}`</SwmToken>.

<SwmSnippet path="/pkg/apiclient/cronworkflow/cron-workflow.proto" line="15">

---

The <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="15:2:2" line-data="message CreateCronWorkflowRequest {">`CreateCronWorkflowRequest`</SwmToken> message structure includes the namespace, the <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="17:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow cronWorkflow = 2;">`CronWorkflow`</SwmToken> definition, and creation options.

```protocol buffer
message CreateCronWorkflowRequest {
  string namespace = 1;
  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflow cronWorkflow = 2;
  k8s.io.apimachinery.pkg.apis.meta.v1.CreateOptions createOptions = 3;
}
```

---

</SwmSnippet>

## <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="72:3:3" line-data="  rpc ListCronWorkflows(ListCronWorkflowsRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflowList) {">`ListCronWorkflows`</SwmToken>

The <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="72:3:3" line-data="  rpc ListCronWorkflows(ListCronWorkflowsRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.CronWorkflowList) {">`ListCronWorkflows`</SwmToken> endpoint allows clients to list all CronWorkflows within a specified namespace. It accepts a <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="21:2:2" line-data="message ListCronWorkflowsRequest {">`ListCronWorkflowsRequest`</SwmToken> message containing the namespace and list options. The corresponding HTTP method is GET, and the URL pattern is <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="61:6:17" line-data="      post : &quot;/api/v1/cron-workflows/{namespace}/lint&quot;">`/api/v1/cron-workflows/{namespace}`</SwmToken>.

<SwmSnippet path="/pkg/apiclient/cronworkflow/cron-workflow.proto" line="21">

---

The <SwmToken path="pkg/apiclient/cronworkflow/cron-workflow.proto" pos="21:2:2" line-data="message ListCronWorkflowsRequest {">`ListCronWorkflowsRequest`</SwmToken> message structure includes the namespace and list options.

```protocol buffer
message ListCronWorkflowsRequest {
  string namespace = 1;
  k8s.io.apimachinery.pkg.apis.meta.v1.ListOptions listOptions = 2;
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
