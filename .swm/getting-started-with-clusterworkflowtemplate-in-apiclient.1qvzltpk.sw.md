---
title: Getting Started with ClusterWorkflowTemplate in Apiclient
---
# Introduction

<SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:36:36" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`ClusterWorkflowTemplate`</SwmToken> is a cluster-scoped resource that defines a workflow template accessible across all namespaces within a Kubernetes cluster. It allows users to create reusable workflow templates that can be referenced and executed from any namespace, similar to how ClusterRoles work. The <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="489:18:18" line-data="	err := c.cc.Invoke(ctx, &quot;/clusterworkflowtemplate.ClusterWorkflowTemplateService/CreateClusterWorkflowTemplate&quot;, in, out, opts...)">`ClusterWorkflowTemplateService`</SwmToken> in the Apiclient package provides CRUD operations for managing these templates, including creating, retrieving, and deleting them. The service translates gRPC calls into RESTful JSON APIs, enabling seamless integration with other services and tools.

# Managing ClusterWorkflowTemplates

You can manage ClusterWorkflowTemplates using CLI, kubectl, or UI. For example, you can create templates using the CLI with <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="13:10:10" line-data="	v1alpha1 &quot;github.com/argoproj/argo-workflows/v3/pkg/apis/workflow/v1alpha1&quot;">`argo`</SwmToken>` cluster-template create` and submit workflows using <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="13:10:10" line-data="	v1alpha1 &quot;github.com/argoproj/argo-workflows/v3/pkg/apis/workflow/v1alpha1&quot;">`argo`</SwmToken>` submit`. Similarly, you can use `kubectl apply -f` and `kubectl `<SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.proto" pos="53:11:11" line-data="    option (google.api.http).get = &quot;/api/v1/cluster-workflow-templates/{name}&quot;;">`get`</SwmToken>` cwft` for managing templates via kubectl.

# Main Functions

The <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="489:18:18" line-data="	err := c.cc.Invoke(ctx, &quot;/clusterworkflowtemplate.ClusterWorkflowTemplateService/CreateClusterWorkflowTemplate&quot;, in, out, opts...)">`ClusterWorkflowTemplateService`</SwmToken> provides CRUD operations for managing ClusterWorkflowTemplates, including creating, retrieving, and deleting them.

## <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:9:9" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`CreateClusterWorkflowTemplate`</SwmToken>

The <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:9:9" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`CreateClusterWorkflowTemplate`</SwmToken> function is used to create a new <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:36:36" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`ClusterWorkflowTemplate`</SwmToken>. It takes a <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:21:21" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`ClusterWorkflowTemplateCreateRequest`</SwmToken> and returns a <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:36:36" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`ClusterWorkflowTemplate`</SwmToken> object.

<SwmSnippet path="/pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" line="487">

---

The function <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:9:9" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`CreateClusterWorkflowTemplate`</SwmToken> creates a new <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:36:36" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`ClusterWorkflowTemplate`</SwmToken> by invoking the gRPC call and returning the created template object.

```go
func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {
	out := new(v1alpha1.ClusterWorkflowTemplate)
	err := c.cc.Invoke(ctx, "/clusterworkflowtemplate.ClusterWorkflowTemplateService/CreateClusterWorkflowTemplate", in, out, opts...)
	if err != nil {
		return nil, err
	}
	return out, nil
```

---

</SwmSnippet>

## <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="496:9:9" line-data="func (c *clusterWorkflowTemplateServiceClient) GetClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateGetRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`GetClusterWorkflowTemplate`</SwmToken>

The <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="496:9:9" line-data="func (c *clusterWorkflowTemplateServiceClient) GetClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateGetRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`GetClusterWorkflowTemplate`</SwmToken> function retrieves an existing <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:36:36" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`ClusterWorkflowTemplate`</SwmToken> by its name. It takes a <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="496:21:21" line-data="func (c *clusterWorkflowTemplateServiceClient) GetClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateGetRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`ClusterWorkflowTemplateGetRequest`</SwmToken> and returns a <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:36:36" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`ClusterWorkflowTemplate`</SwmToken> object.

<SwmSnippet path="/pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" line="496">

---

The function <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="496:9:9" line-data="func (c *clusterWorkflowTemplateServiceClient) GetClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateGetRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`GetClusterWorkflowTemplate`</SwmToken> retrieves a <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="496:36:36" line-data="func (c *clusterWorkflowTemplateServiceClient) GetClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateGetRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`ClusterWorkflowTemplate`</SwmToken> by its name by invoking the gRPC call and returning the retrieved template object.

```go
func (c *clusterWorkflowTemplateServiceClient) GetClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateGetRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {
	out := new(v1alpha1.ClusterWorkflowTemplate)
	err := c.cc.Invoke(ctx, "/clusterworkflowtemplate.ClusterWorkflowTemplateService/GetClusterWorkflowTemplate", in, out, opts...)
	if err != nil {
		return nil, err
	}
	return out, nil
```

---

</SwmSnippet>

## <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="475:1:1" line-data="	DeleteClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateDeleteRequest, opts ...grpc.CallOption) (*ClusterWorkflowTemplateDeleteResponse, error)">`DeleteClusterWorkflowTemplate`</SwmToken>

The <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="475:1:1" line-data="	DeleteClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateDeleteRequest, opts ...grpc.CallOption) (*ClusterWorkflowTemplateDeleteResponse, error)">`DeleteClusterWorkflowTemplate`</SwmToken> function deletes an existing <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:36:36" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`ClusterWorkflowTemplate`</SwmToken> by its name. It takes a <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="250:2:2" line-data="type ClusterWorkflowTemplateDeleteRequest struct {">`ClusterWorkflowTemplateDeleteRequest`</SwmToken> and returns a <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="305:2:2" line-data="type ClusterWorkflowTemplateDeleteResponse struct {">`ClusterWorkflowTemplateDeleteResponse`</SwmToken>.

<SwmSnippet path="/pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" line="268">

---

The function <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="475:1:1" line-data="	DeleteClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateDeleteRequest, opts ...grpc.CallOption) (*ClusterWorkflowTemplateDeleteResponse, error)">`DeleteClusterWorkflowTemplate`</SwmToken> deletes a <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:36:36" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`ClusterWorkflowTemplate`</SwmToken> by its name by invoking the gRPC call and returning the delete response.

```go
	if deterministic {
		return xxx_messageInfo_ClusterWorkflowTemplateDeleteRequest.Marshal(b, m, deterministic)
	} else {
		b = b[:cap(b)]
		n, err := m.MarshalToSizedBuffer(b)
		if err != nil {
			return nil, err
		}
		return b[:n], nil
```

---

</SwmSnippet>

# <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:36:36" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`ClusterWorkflowTemplate`</SwmToken> Endpoints

The <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="489:18:18" line-data="	err := c.cc.Invoke(ctx, &quot;/clusterworkflowtemplate.ClusterWorkflowTemplateService/CreateClusterWorkflowTemplate&quot;, in, out, opts...)">`ClusterWorkflowTemplateService`</SwmToken> provides several endpoints for managing ClusterWorkflowTemplates.

## <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:9:9" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`CreateClusterWorkflowTemplate`</SwmToken>

The <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:9:9" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`CreateClusterWorkflowTemplate`</SwmToken> endpoint allows users to create a new <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:36:36" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`ClusterWorkflowTemplate`</SwmToken>. It uses the HTTP POST method and the URL <SwmPath>[ui/src/app/cluster-workflow-templates/](ui/src/app/cluster-workflow-templates/)</SwmPath>. The request body should contain the template details.

<SwmSnippet path="/pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.proto" line="45">

---

The <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.proto" pos="45:3:3" line-data="  rpc CreateClusterWorkflowTemplate(ClusterWorkflowTemplateCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.ClusterWorkflowTemplate) {">`CreateClusterWorkflowTemplate`</SwmToken> endpoint is defined in the proto file, specifying the HTTP POST method and the URL for creating a new <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.proto" pos="45:29:29" line-data="  rpc CreateClusterWorkflowTemplate(ClusterWorkflowTemplateCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.ClusterWorkflowTemplate) {">`ClusterWorkflowTemplate`</SwmToken>.

```protocol buffer
  rpc CreateClusterWorkflowTemplate(ClusterWorkflowTemplateCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.ClusterWorkflowTemplate) {
    option (google.api.http) = {
      post : "/api/v1/cluster-workflow-templates"
      body : "*"
    };
  }
```

---

</SwmSnippet>

## <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="496:9:9" line-data="func (c *clusterWorkflowTemplateServiceClient) GetClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateGetRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`GetClusterWorkflowTemplate`</SwmToken>

The <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="496:9:9" line-data="func (c *clusterWorkflowTemplateServiceClient) GetClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateGetRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`GetClusterWorkflowTemplate`</SwmToken> endpoint retrieves a specific <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.pb.go" pos="487:36:36" line-data="func (c *clusterWorkflowTemplateServiceClient) CreateClusterWorkflowTemplate(ctx context.Context, in *ClusterWorkflowTemplateCreateRequest, opts ...grpc.CallOption) (*v1alpha1.ClusterWorkflowTemplate, error) {">`ClusterWorkflowTemplate`</SwmToken> by its name. It uses the HTTP GET method and the URL <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.proto" pos="53:16:29" line-data="    option (google.api.http).get = &quot;/api/v1/cluster-workflow-templates/{name}&quot;;">`/api/v1/cluster-workflow-templates/{name}`</SwmToken>. The request should include the name of the template to be retrieved.

<SwmSnippet path="/pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.proto" line="52">

---

The <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.proto" pos="52:3:3" line-data="  rpc GetClusterWorkflowTemplate(ClusterWorkflowTemplateGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.ClusterWorkflowTemplate) {">`GetClusterWorkflowTemplate`</SwmToken> endpoint is defined in the proto file, specifying the HTTP GET method and the URL for retrieving a <SwmToken path="pkg/apiclient/clusterworkflowtemplate/cluster-workflow-template.proto" pos="52:29:29" line-data="  rpc GetClusterWorkflowTemplate(ClusterWorkflowTemplateGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.ClusterWorkflowTemplate) {">`ClusterWorkflowTemplate`</SwmToken> by its name.

```protocol buffer
  rpc GetClusterWorkflowTemplate(ClusterWorkflowTemplateGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.ClusterWorkflowTemplate) {
    option (google.api.http).get = "/api/v1/cluster-workflow-templates/{name}";
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
