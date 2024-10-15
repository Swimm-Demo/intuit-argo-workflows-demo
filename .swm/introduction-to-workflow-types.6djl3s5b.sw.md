---
title: Introduction to Workflow Types
---
# Introduction to Workflow Types

Workflow types refer to the different structures and configurations that define how workflows are executed. These types include the overall workflow structure, individual workflow steps, and the metadata associated with workflows.

# Workflow Type

The <SwmToken path="pkg/apis/workflow/v1alpha1/workflow_types.go" pos="267:14:14" line-data="// WorkflowSpec is the specification of a Workflow.">`Workflow`</SwmToken> type defines the overall structure of a workflow resource, including its metadata, specifications, and status. It serves as the primary resource for managing workflows.

# <SwmToken path="pkg/apis/workflow/v1alpha1/workflow_types.go" pos="1490:2:2" line-data="// WorkflowStep is a reference to a template to execute in a series of step">`WorkflowStep`</SwmToken> Type

The <SwmToken path="pkg/apis/workflow/v1alpha1/workflow_types.go" pos="1490:2:2" line-data="// WorkflowStep is a reference to a template to execute in a series of step">`WorkflowStep`</SwmToken> type represents individual steps within a workflow. Each step can reference a template to execute, hold arguments, and define conditions for execution.

<SwmSnippet path="/pkg/apis/workflow/v1alpha1/workflow_types.go" line="1490">

---

The <SwmToken path="pkg/apis/workflow/v1alpha1/workflow_types.go" pos="1490:2:2" line-data="// WorkflowStep is a reference to a template to execute in a series of step">`WorkflowStep`</SwmToken> type is defined in the code, detailing how each step can reference a template, hold arguments, and define execution conditions.

```go
// WorkflowStep is a reference to a template to execute in a series of step
type WorkflowStep struct {
	// Name of the step
	Name string `json:"name,omitempty" protobuf:"bytes,1,opt,name=name"`

	// Template is the name of the template to execute as the step
	Template string `json:"template,omitempty" protobuf:"bytes,2,opt,name=template"`

	// Inline is the template. Template must be empty if this is declared (and vice-versa).
	Inline *Template `json:"inline,omitempty" protobuf:"bytes,13,opt,name=inline"`

	// Arguments hold arguments to the template
	Arguments Arguments `json:"arguments,omitempty" protobuf:"bytes,3,opt,name=arguments"`

	// TemplateRef is the reference to the template resource to execute as the step.
	TemplateRef *TemplateRef `json:"templateRef,omitempty" protobuf:"bytes,4,opt,name=templateRef"`

	// WithItems expands a step into multiple parallel steps from the items in the list
	WithItems []Item `json:"withItems,omitempty" protobuf:"bytes,5,rep,name=withItems"`

	// WithParam expands a step into multiple parallel steps from the value in the parameter,
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apis/workflow/v1alpha1/workflow_types.go" line="267">

---

The <SwmToken path="pkg/apis/workflow/v1alpha1/workflow_types.go" pos="267:2:2" line-data="// WorkflowSpec is the specification of a Workflow.">`WorkflowSpec`</SwmToken> type is defined in the code, specifying the details of a workflow, including templates, entry points, arguments, and configurations.

```go
// WorkflowSpec is the specification of a Workflow.
type WorkflowSpec struct {
	// Templates is a list of workflow templates used in a workflow
	// +patchStrategy=merge
	// +patchMergeKey=name
	Templates []Template `json:"templates,omitempty" patchStrategy:"merge" patchMergeKey:"name" protobuf:"bytes,1,opt,name=templates"`

	// Entrypoint is a template reference to the starting point of the workflow.
	Entrypoint string `json:"entrypoint,omitempty" protobuf:"bytes,2,opt,name=entrypoint"`

	// Arguments contain the parameters and artifacts sent to the workflow entrypoint
	// Parameters are referencable globally using the 'workflow' variable prefix.
	// e.g. {{workflow.parameters.myparam}}
	Arguments Arguments `json:"arguments,omitempty" protobuf:"bytes,3,opt,name=arguments"`

	// ServiceAccountName is the name of the ServiceAccount to run all pods of the workflow as.
	ServiceAccountName string `json:"serviceAccountName,omitempty" protobuf:"bytes,4,opt,name=serviceAccountName"`

	// AutomountServiceAccountToken indicates whether a service account token should be automatically mounted in pods.
	// ServiceAccountName of ExecutorConfig must be specified if this value is false.
	AutomountServiceAccountToken *bool `json:"automountServiceAccountToken,omitempty" protobuf:"varint,28,opt,name=automountServiceAccountToken"`
```

---

</SwmSnippet>

# <SwmToken path="pkg/apis/workflow/v1alpha1/workflow_types.go" pos="155:3:3" line-data="	Status            WorkflowStatus `json:&quot;status,omitempty&quot; protobuf:&quot;bytes,3,opt,name=status&quot;`">`WorkflowStatus`</SwmToken> Type

The <SwmToken path="pkg/apis/workflow/v1alpha1/workflow_types.go" pos="155:3:3" line-data="	Status            WorkflowStatus `json:&quot;status,omitempty&quot; protobuf:&quot;bytes,3,opt,name=status&quot;`">`WorkflowStatus`</SwmToken> type contains information about the current state of a workflow, including its phase, start and end times, progress, and any messages or conditions.

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
