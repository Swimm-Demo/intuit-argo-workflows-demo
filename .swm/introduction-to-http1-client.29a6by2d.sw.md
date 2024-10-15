---
title: Introduction to Http1 Client
---
# Introduction to Http1 Client

The Http1 package within the Apiclient directory provides various client functionalities for interacting with different services. This package includes multiple client implementations such as `info-service-client`, `watch-workflows-client`, `server-sent-events-client`, and `workflow-service-client`.

# Facade Struct

The <SwmToken path="pkg/apiclient/http1/archived-workflows-service-client.go" pos="13:6:6" line-data="type ArchivedWorkflowsServiceClient = Facade">`Facade`</SwmToken> struct encapsulates common HTTP operations like GET, POST, PUT, and DELETE, making it easier to interact with RESTful APIs.

# Server-Sent Events Client

The `serverSentEventsClient` struct is designed to handle Server-Sent Events (SSE), providing a consistent way to receive real-time updates from the server.

# Specialized Clients

The package also includes specialized clients for handling events and logs, such as `eventWatchClient` and `podLogsClient`, which facilitate streaming and monitoring of workflow-related events and logs.

# HTTPHeader

HTTPHeader describes a custom header to be used in HTTP probes.

# Http1 Endpoints

The Http1 package defines various endpoints for interacting with different services.

<SwmSnippet path="/pkg/apiclient/http1/archived-workflows-service-client.go" line="15">

---

## <SwmToken path="pkg/apiclient/http1/archived-workflows-service-client.go" pos="15:8:8" line-data="func (h ArchivedWorkflowsServiceClient) ListArchivedWorkflows(ctx context.Context, in *workflowarchivepkg.ListArchivedWorkflowsRequest, _ ...grpc.CallOption) (*wfv1.WorkflowList, error) {">`ListArchivedWorkflows`</SwmToken>

The <SwmToken path="pkg/apiclient/http1/archived-workflows-service-client.go" pos="15:8:8" line-data="func (h ArchivedWorkflowsServiceClient) ListArchivedWorkflows(ctx context.Context, in *workflowarchivepkg.ListArchivedWorkflowsRequest, _ ...grpc.CallOption) (*wfv1.WorkflowList, error) {">`ListArchivedWorkflows`</SwmToken> function is an endpoint that retrieves a list of archived workflows. It uses the GET method to access the <SwmToken path="pkg/apiclient/http1/archived-workflows-service-client.go" pos="17:20:27" line-data="	return out, h.Get(ctx, in, out, &quot;/api/v1/archived-workflows&quot;)">`/api/v1/archived-workflows`</SwmToken> URL.

```go
func (h ArchivedWorkflowsServiceClient) ListArchivedWorkflows(ctx context.Context, in *workflowarchivepkg.ListArchivedWorkflowsRequest, _ ...grpc.CallOption) (*wfv1.WorkflowList, error) {
	out := &wfv1.WorkflowList{}
	return out, h.Get(ctx, in, out, "/api/v1/archived-workflows")
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apiclient/http1/workflow-template-service-client.go" line="14">

---

## <SwmToken path="pkg/apiclient/http1/workflow-template-service-client.go" pos="14:8:8" line-data="func (h WorkflowTemplateServiceClient) CreateWorkflowTemplate(ctx context.Context, in *workflowtemplatepkg.WorkflowTemplateCreateRequest, _ ...grpc.CallOption) (*wfv1.WorkflowTemplate, error) {">`CreateWorkflowTemplate`</SwmToken>

The <SwmToken path="pkg/apiclient/http1/workflow-template-service-client.go" pos="14:8:8" line-data="func (h WorkflowTemplateServiceClient) CreateWorkflowTemplate(ctx context.Context, in *workflowtemplatepkg.WorkflowTemplateCreateRequest, _ ...grpc.CallOption) (*wfv1.WorkflowTemplate, error) {">`CreateWorkflowTemplate`</SwmToken> function is an endpoint that creates a new workflow template. It uses the POST method to access the <SwmToken path="pkg/apiclient/http1/workflow-template-service-client.go" pos="16:20:31" line-data="	return out, h.Post(ctx, in, out, &quot;/api/v1/workflow-templates/{namespace}&quot;)">`/api/v1/workflow-templates/{namespace}`</SwmToken> URL.

```go
func (h WorkflowTemplateServiceClient) CreateWorkflowTemplate(ctx context.Context, in *workflowtemplatepkg.WorkflowTemplateCreateRequest, _ ...grpc.CallOption) (*wfv1.WorkflowTemplate, error) {
	out := &wfv1.WorkflowTemplate{}
	return out, h.Post(ctx, in, out, "/api/v1/workflow-templates/{namespace}")
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
