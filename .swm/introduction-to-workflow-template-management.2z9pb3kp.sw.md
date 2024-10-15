---
title: Introduction to Workflow Template Management
---
# Introduction to Workflow Template Management

Workflow templates are a key component in Argo Workflows, enabling users to define reusable workflows. These templates can be managed using the `WorkflowTemplateServiceClient` interface, which provides methods for creating, retrieving, listing, updating, deleting, and linting workflow templates.

# Managing Workflow Templates

You can manage workflow templates using the Argo CLI. For example, to create templates, use the command <SwmPath>[examples/workflow-template/templates.yaml](examples/workflow-template/templates.yaml)</SwmPath>. To submit a workflow using one of these templates, use <SwmPath>[examples/workflow-template/hello-world.yaml](examples/workflow-template/hello-world.yaml)</SwmPath>.

# Submitting Workflow Templates

To submit a <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="15:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate template = 2;">`WorkflowTemplate`</SwmToken> as a Workflow, use the command <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="2:13:13" line-data="option go_package = &quot;github.com/argoproj/argo-workflows/pkg/apiclient/workflowtemplate&quot;;">`argo`</SwmToken>` submit --from workflowtemplate/workflow-template-submittable`. If you need to submit a <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="15:19:19" line-data="  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate template = 2;">`WorkflowTemplate`</SwmToken> with parameters, use <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="2:13:13" line-data="option go_package = &quot;github.com/argoproj/argo-workflows/pkg/apiclient/workflowtemplate&quot;;">`argo`</SwmToken>` submit --from workflowtemplate/workflow-template-submittable -p message=value1`.

# Defining Workflow Templates

To define your workflow as a workflow template, use the following YAML structure:

- <SwmPath>[pkg/apis/workflow/v1alpha1/](pkg/apis/workflow/v1alpha1/)</SwmPath>
- `kind: `<SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="59:29:29" line-data="  rpc GetWorkflowTemplate(WorkflowTemplateGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`WorkflowTemplate`</SwmToken>
- `metadata: `<SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="20:3:3" line-data="  string name = 1;">`name`</SwmToken>`: workflow-template-submittable`
- `spec: entrypoint: print-message`
- `arguments: parameters: - `<SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="20:3:3" line-data="  string name = 1;">`name`</SwmToken>`: `<SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="13:0:0" line-data="message WorkflowTemplateCreateRequest {">`message`</SwmToken>` value: hello world`
- <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="54:13:13" line-data="      post : &quot;/api/v1/workflow-templates/{namespace}&quot;">`templates`</SwmToken>`: - `<SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="20:3:3" line-data="  string name = 1;">`name`</SwmToken>`: print-message inputs: parameters: - `<SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="20:3:3" line-data="  string name = 1;">`name`</SwmToken>`: `<SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="13:0:0" line-data="message WorkflowTemplateCreateRequest {">`message`</SwmToken>` container: image: busybox command: [echo] args: ["{{inputs.parameters.message}}"]`

# Main Functions

The main functions for managing workflow templates include <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="52:3:3" line-data="  rpc CreateWorkflowTemplate(WorkflowTemplateCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`CreateWorkflowTemplate`</SwmToken>, <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="59:3:3" line-data="  rpc GetWorkflowTemplate(WorkflowTemplateGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`GetWorkflowTemplate`</SwmToken>, <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="63:3:3" line-data="  rpc ListWorkflowTemplates(WorkflowTemplateListRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplateList) {">`ListWorkflowTemplates`</SwmToken>, <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="67:3:3" line-data="  rpc UpdateWorkflowTemplate(WorkflowTemplateUpdateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`UpdateWorkflowTemplate`</SwmToken>, <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="74:3:3" line-data="  rpc DeleteWorkflowTemplate(WorkflowTemplateDeleteRequest) returns (WorkflowTemplateDeleteResponse) {">`DeleteWorkflowTemplate`</SwmToken>, and <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="78:3:3" line-data="  rpc LintWorkflowTemplate(WorkflowTemplateLintRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`LintWorkflowTemplate`</SwmToken>. Below, we will dive into each of these functions.

<SwmSnippet path="/pkg/apiclient/workflowtemplate/workflow-template.proto" line="13">

---

## <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="52:3:3" line-data="  rpc CreateWorkflowTemplate(WorkflowTemplateCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`CreateWorkflowTemplate`</SwmToken>

The <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="52:3:3" line-data="  rpc CreateWorkflowTemplate(WorkflowTemplateCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`CreateWorkflowTemplate`</SwmToken> function is used to create a new workflow template. It takes a <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="13:2:2" line-data="message WorkflowTemplateCreateRequest {">`WorkflowTemplateCreateRequest`</SwmToken> message as input, which includes the namespace and the workflow template definition.

```protocol buffer
message WorkflowTemplateCreateRequest {
  string namespace = 1;
  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate template = 2;
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apiclient/workflowtemplate/workflow-template.proto" line="19">

---

## <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="59:3:3" line-data="  rpc GetWorkflowTemplate(WorkflowTemplateGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`GetWorkflowTemplate`</SwmToken>

The <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="59:3:3" line-data="  rpc GetWorkflowTemplate(WorkflowTemplateGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`GetWorkflowTemplate`</SwmToken> function retrieves a workflow template by its name and namespace. It uses a <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="19:2:2" line-data="message WorkflowTemplateGetRequest {">`WorkflowTemplateGetRequest`</SwmToken> message to specify the template's name and namespace.

```protocol buffer
message WorkflowTemplateGetRequest {
  string name = 1;
  string namespace = 2;
  k8s.io.apimachinery.pkg.apis.meta.v1.GetOptions getOptions = 3;
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apiclient/workflowtemplate/workflow-template.proto" line="25">

---

## <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="63:3:3" line-data="  rpc ListWorkflowTemplates(WorkflowTemplateListRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplateList) {">`ListWorkflowTemplates`</SwmToken>

The <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="63:3:3" line-data="  rpc ListWorkflowTemplates(WorkflowTemplateListRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplateList) {">`ListWorkflowTemplates`</SwmToken> function lists all workflow templates in a specified namespace. It uses a <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="25:2:2" line-data="message WorkflowTemplateListRequest {">`WorkflowTemplateListRequest`</SwmToken> message to filter the templates by namespace and name pattern.

```protocol buffer
message WorkflowTemplateListRequest {
  string namespace = 1;
  string namePattern = 2;
  k8s.io.apimachinery.pkg.apis.meta.v1.ListOptions listOptions = 3;
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apiclient/workflowtemplate/workflow-template.proto" line="31">

---

## <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="67:3:3" line-data="  rpc UpdateWorkflowTemplate(WorkflowTemplateUpdateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`UpdateWorkflowTemplate`</SwmToken>

The <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="67:3:3" line-data="  rpc UpdateWorkflowTemplate(WorkflowTemplateUpdateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`UpdateWorkflowTemplate`</SwmToken> function updates an existing workflow template. It takes a <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="31:2:2" line-data="message WorkflowTemplateUpdateRequest {">`WorkflowTemplateUpdateRequest`</SwmToken> message, which includes the namespace and the updated workflow template definition.

```protocol buffer
message WorkflowTemplateUpdateRequest {
  // DEPRECATED: This field is ignored.
  string name = 1 [ deprecated = true ];
  string namespace = 2;
  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate template = 3;
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apiclient/workflowtemplate/workflow-template.proto" line="38">

---

## <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="74:3:3" line-data="  rpc DeleteWorkflowTemplate(WorkflowTemplateDeleteRequest) returns (WorkflowTemplateDeleteResponse) {">`DeleteWorkflowTemplate`</SwmToken>

The <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="74:3:3" line-data="  rpc DeleteWorkflowTemplate(WorkflowTemplateDeleteRequest) returns (WorkflowTemplateDeleteResponse) {">`DeleteWorkflowTemplate`</SwmToken> function deletes a workflow template by its name and namespace. It uses a <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="38:2:2" line-data="message WorkflowTemplateDeleteRequest {">`WorkflowTemplateDeleteRequest`</SwmToken> message to specify the template's name and namespace.

```protocol buffer
message WorkflowTemplateDeleteRequest {
  string name = 1;
  string namespace = 2;
  k8s.io.apimachinery.pkg.apis.meta.v1.DeleteOptions deleteOptions = 3;
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apiclient/workflowtemplate/workflow-template.proto" line="45">

---

## <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="78:3:3" line-data="  rpc LintWorkflowTemplate(WorkflowTemplateLintRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`LintWorkflowTemplate`</SwmToken>

The <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="78:3:3" line-data="  rpc LintWorkflowTemplate(WorkflowTemplateLintRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`LintWorkflowTemplate`</SwmToken> function checks the syntax and validity of a workflow template without actually creating it. It uses a <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="45:2:2" line-data="message WorkflowTemplateLintRequest {">`WorkflowTemplateLintRequest`</SwmToken> message, which includes the namespace and the workflow template definition.

```protocol buffer
message WorkflowTemplateLintRequest {
  string namespace = 1;
  github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate template = 2;
  k8s.io.apimachinery.pkg.apis.meta.v1.CreateOptions createOptions = 3;
}
```

---

</SwmSnippet>

# Workflow Template APIs

The Workflow Template APIs provide endpoints for managing workflow templates. These include creating, retrieving, listing, updating, deleting, and linting workflow templates.

<SwmSnippet path="/pkg/apiclient/workflowtemplate/workflow-template.proto" line="52">

---

## <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="52:3:3" line-data="  rpc CreateWorkflowTemplate(WorkflowTemplateCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`CreateWorkflowTemplate`</SwmToken> API

The <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="52:3:3" line-data="  rpc CreateWorkflowTemplate(WorkflowTemplateCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`CreateWorkflowTemplate`</SwmToken> endpoint allows users to create a new workflow template. It accepts a <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="52:5:5" line-data="  rpc CreateWorkflowTemplate(WorkflowTemplateCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`WorkflowTemplateCreateRequest`</SwmToken> message and returns the created <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="52:29:29" line-data="  rpc CreateWorkflowTemplate(WorkflowTemplateCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`WorkflowTemplate`</SwmToken>. The HTTP method used is POST, and the URL pattern is <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="54:6:17" line-data="      post : &quot;/api/v1/workflow-templates/{namespace}&quot;">`/api/v1/workflow-templates/{namespace}`</SwmToken>.

```protocol buffer
  rpc CreateWorkflowTemplate(WorkflowTemplateCreateRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {
    option (google.api.http) = {
      post : "/api/v1/workflow-templates/{namespace}"
      body : "*"
    };
  }
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apiclient/workflowtemplate/workflow-template.proto" line="59">

---

## <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="59:3:3" line-data="  rpc GetWorkflowTemplate(WorkflowTemplateGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`GetWorkflowTemplate`</SwmToken> API

The <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="59:3:3" line-data="  rpc GetWorkflowTemplate(WorkflowTemplateGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`GetWorkflowTemplate`</SwmToken> endpoint retrieves a specific workflow template by its name and namespace. It accepts a <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="59:5:5" line-data="  rpc GetWorkflowTemplate(WorkflowTemplateGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`WorkflowTemplateGetRequest`</SwmToken> message and returns the requested <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="59:29:29" line-data="  rpc GetWorkflowTemplate(WorkflowTemplateGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {">`WorkflowTemplate`</SwmToken>. The HTTP method used is GET, and the URL pattern is <SwmToken path="pkg/apiclient/workflowtemplate/workflow-template.proto" pos="60:16:31" line-data="    option (google.api.http).get = &quot;/api/v1/workflow-templates/{namespace}/{name}&quot;;">`/api/v1/workflow-templates/{namespace}/{name}`</SwmToken>.

```protocol buffer
  rpc GetWorkflowTemplate(WorkflowTemplateGetRequest) returns (github.com.argoproj.argo_workflows.v3.pkg.apis.workflow.v1alpha1.WorkflowTemplate) {
    option (google.api.http).get = "/api/v1/workflow-templates/{namespace}/{name}";
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
