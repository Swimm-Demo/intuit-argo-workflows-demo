---
title: Understanding Workflow Management
---
## Overview

In Apiclient, workflows are managed through various CRUD operations.

## <SwmToken path="pkg/apiclient/workflow/workflow.pb.go" pos="1417:2:2" line-data="// WorkflowServiceClient is the client API for WorkflowService service.">`WorkflowServiceClient`</SwmToken> Interface

The <SwmToken path="pkg/apiclient/workflow/workflow.pb.go" pos="1417:2:2" line-data="// WorkflowServiceClient is the client API for WorkflowService service.">`WorkflowServiceClient`</SwmToken> interface provides methods to create, retrieve, list, and delete workflows. It also supports operations like retrying, resubmitting, suspending, and terminating workflows.

## Workflow Requests

Different types of requests are used to manage workflows:

- <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="139:5:5" line-data="  rpc CreateWorkflow(WorkflowCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.Workflow) {">`WorkflowCreateRequest`</SwmToken>: Used to create a new workflow, specifying details like namespace and workflow definition.
- <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="146:5:5" line-data="  rpc GetWorkflow(WorkflowGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.Workflow) {">`WorkflowGetRequest`</SwmToken>: Retrieves details of a specific workflow, identified by its name and namespace.
- <SwmToken path="pkg/apiclient/workflow/workflow.pb.go" pos="190:2:2" line-data="type WorkflowListRequest struct {">`WorkflowListRequest`</SwmToken>: Lists all workflows within a specified namespace, with options to filter the results.
- <SwmToken path="pkg/apiclient/workflow/workflow.pb.go" pos="254:2:2" line-data="type WorkflowResubmitRequest struct {">`WorkflowResubmitRequest`</SwmToken> and <SwmToken path="pkg/apiclient/workflow/workflow.pb.go" pos="325:2:2" line-data="type WorkflowRetryRequest struct {">`WorkflowRetryRequest`</SwmToken>: Handle resubmitting and retrying workflows, respectively, with options to modify parameters.
- <SwmToken path="pkg/apiclient/workflow/workflow.pb.go" pos="680:2:2" line-data="type WorkflowSuspendRequest struct {">`WorkflowSuspendRequest`</SwmToken>, <SwmToken path="pkg/apiclient/workflow/workflow.pb.go" pos="404:2:2" line-data="type WorkflowResumeRequest struct {">`WorkflowResumeRequest`</SwmToken>, and <SwmToken path="pkg/apiclient/workflow/workflow.pb.go" pos="467:2:2" line-data="type WorkflowTerminateRequest struct {">`WorkflowTerminateRequest`</SwmToken>: Manage the state of workflows, allowing them to be suspended, resumed, or terminated.

## Real-time Updates

The <SwmToken path="pkg/apiclient/workflow/workflow.pb.go" pos="1417:2:2" line-data="// WorkflowServiceClient is the client API for WorkflowService service.">`WorkflowServiceClient`</SwmToken> interface also includes methods for watching workflow events and logs, providing real-time updates on workflow execution.

## Workflow of Workflows

The Workflow of Workflows pattern involves a parent workflow triggering one or more child workflows, managing them, and acting on their results.

## Examples

You can use `workflowTemplateRef` to trigger a workflow inline. First, define your workflow as a `workflowtemplate`.

<SwmSnippet path="/pkg/apiclient/workflow/workflow.pb.go" line="39">

---

The <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="139:5:5" line-data="  rpc CreateWorkflow(WorkflowCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.Workflow) {">`WorkflowCreateRequest`</SwmToken> message is used to create a new workflow, specifying details like namespace and workflow definition.

```go
	Workflow  *v1alpha1.Workflow `protobuf:"bytes,2,opt,name=workflow,proto3" json:"workflow,omitempty"`
	// This field is no longer used.
	InstanceID           string            `protobuf:"bytes,3,opt,name=instanceID,proto3" json:"instanceID,omitempty"` // Deprecated: Do not use.
	ServerDryRun         bool              `protobuf:"varint,4,opt,name=serverDryRun,proto3" json:"serverDryRun,omitempty"`
	CreateOptions        *v1.CreateOptions `protobuf:"bytes,5,opt,name=createOptions,proto3" json:"createOptions,omitempty"`
	XXX_NoUnkeyedLiteral struct{}          `json:"-"`
	XXX_unrecognized     []byte            `json:"-"`
	XXX_sizecache        int32             `json:"-"`
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apiclient/workflow/workflow.proto" line="138">

---

The <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="138:2:2" line-data="service WorkflowService {">`WorkflowService`</SwmToken> API performs CRUD actions against application resources, including creating workflows.

```protocol buffer
service WorkflowService {
  rpc CreateWorkflow(WorkflowCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.Workflow) {
    option (google.api.http) = {
```

---

</SwmSnippet>

## Workflow APIs

Workflow APIs provide endpoints for managing workflows.

### <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="139:3:3" line-data="  rpc CreateWorkflow(WorkflowCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.Workflow) {">`CreateWorkflow`</SwmToken>

The <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="139:3:3" line-data="  rpc CreateWorkflow(WorkflowCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.Workflow) {">`CreateWorkflow`</SwmToken> endpoint is used to create a new workflow. It accepts a <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="139:5:5" line-data="  rpc CreateWorkflow(WorkflowCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.Workflow) {">`WorkflowCreateRequest`</SwmToken> message that includes the namespace and workflow definition. The endpoint is accessed via a POST request to <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="141:6:15" line-data="      post : &quot;/api/v1/workflows/{namespace}&quot;">`/api/v1/workflows/{namespace}`</SwmToken>.

<SwmSnippet path="/pkg/apiclient/workflow/workflow.proto" line="138">

---

The <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="139:3:3" line-data="  rpc CreateWorkflow(WorkflowCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.Workflow) {">`CreateWorkflow`</SwmToken> endpoint is defined in the <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="138:2:2" line-data="service WorkflowService {">`WorkflowService`</SwmToken>.

```protocol buffer
service WorkflowService {
  rpc CreateWorkflow(WorkflowCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.Workflow) {
    option (google.api.http) = {
      post : "/api/v1/workflows/{namespace}"
      body : "*"
    };
```

---

</SwmSnippet>

### <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="146:3:3" line-data="  rpc GetWorkflow(WorkflowGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.Workflow) {">`GetWorkflow`</SwmToken>

The <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="146:3:3" line-data="  rpc GetWorkflow(WorkflowGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.Workflow) {">`GetWorkflow`</SwmToken> endpoint retrieves the details of a specific workflow identified by its name and namespace. It uses a <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="146:5:5" line-data="  rpc GetWorkflow(WorkflowGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.Workflow) {">`WorkflowGetRequest`</SwmToken> message and is accessed via a GET request to <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="147:16:29" line-data="    option (google.api.http).get = &quot;/api/v1/workflows/{namespace}/{name}&quot;;">`/api/v1/workflows/{namespace}/{name}`</SwmToken>.

<SwmSnippet path="/pkg/apiclient/workflow/workflow.proto" line="146">

---

The <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="146:3:3" line-data="  rpc GetWorkflow(WorkflowGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.Workflow) {">`GetWorkflow`</SwmToken> endpoint is defined in the <SwmToken path="pkg/apiclient/workflow/workflow.proto" pos="138:2:2" line-data="service WorkflowService {">`WorkflowService`</SwmToken>.

```protocol buffer
  rpc GetWorkflow(WorkflowGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.Workflow) {
    option (google.api.http).get = "/api/v1/workflows/{namespace}/{name}";
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
