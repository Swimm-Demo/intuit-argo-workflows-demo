---
title: Introduction to Workflow Listers
---
# Introduction to Workflow Listers

Workflow listers are essential components used to list and retrieve various workflow-related objects from the indexer. They provide a structured way to access workflow data within Kubernetes environments.

# Workflow Lister

The <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflow.go" pos="28:10:10" line-data="// NewWorkflowLister returns a new WorkflowLister.">`WorkflowLister`</SwmToken> interface defines methods for listing workflows and retrieving workflow objects by namespace. The <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflow.go" pos="30:4:4" line-data="	return &amp;workflowLister{indexer: indexer}">`workflowLister`</SwmToken> struct implements this interface and uses a cache indexer to perform its operations.

<SwmSnippet path="/pkg/client/listers/workflow/v1alpha1/workflow.go" line="28">

---

The <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflow.go" pos="28:2:2" line-data="// NewWorkflowLister returns a new WorkflowLister.">`NewWorkflowLister`</SwmToken> function returns a new instance of <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflow.go" pos="30:4:4" line-data="	return &amp;workflowLister{indexer: indexer}">`workflowLister`</SwmToken>, initializing it with the provided indexer.

```go
// NewWorkflowLister returns a new WorkflowLister.
func NewWorkflowLister(indexer cache.Indexer) WorkflowLister {
	return &workflowLister{indexer: indexer}
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/informers/externalversions/workflow/v1alpha1/workflow.go" line="72">

---

<SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflow.go" pos="73:5:5" line-data="	return v1alpha1.NewWorkflowLister(f.Informer().GetIndexer())">`NewWorkflowLister`</SwmToken> is used within the <SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflow.go" pos="72:9:9" line-data="func (f *workflowInformer) Lister() v1alpha1.WorkflowLister {">`Lister`</SwmToken> function of <SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflow.go" pos="72:6:6" line-data="func (f *workflowInformer) Lister() v1alpha1.WorkflowLister {">`workflowInformer`</SwmToken> to provide access to the indexed workflow data.

```go
func (f *workflowInformer) Lister() v1alpha1.WorkflowLister {
	return v1alpha1.NewWorkflowLister(f.Informer().GetIndexer())
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/listers/workflow/v1alpha1/cronworkflow.go" line="28">

---

The <SwmToken path="pkg/client/listers/workflow/v1alpha1/cronworkflow.go" pos="28:2:2" line-data="// NewCronWorkflowLister returns a new CronWorkflowLister.">`NewCronWorkflowLister`</SwmToken> function initializes a new <SwmToken path="pkg/client/listers/workflow/v1alpha1/cronworkflow.go" pos="30:4:4" line-data="	return &amp;cronWorkflowLister{indexer: indexer}">`cronWorkflowLister`</SwmToken> with the provided indexer.

```go
// NewCronWorkflowLister returns a new CronWorkflowLister.
func NewCronWorkflowLister(indexer cache.Indexer) CronWorkflowLister {
	return &cronWorkflowLister{indexer: indexer}
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/informers/externalversions/workflow/v1alpha1/cronworkflow.go" line="72">

---

<SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/cronworkflow.go" pos="73:5:5" line-data="	return v1alpha1.NewCronWorkflowLister(f.Informer().GetIndexer())">`NewCronWorkflowLister`</SwmToken> is used within the <SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/cronworkflow.go" pos="72:9:9" line-data="func (f *cronWorkflowInformer) Lister() v1alpha1.CronWorkflowLister {">`Lister`</SwmToken> function of <SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/cronworkflow.go" pos="72:6:6" line-data="func (f *cronWorkflowInformer) Lister() v1alpha1.CronWorkflowLister {">`cronWorkflowInformer`</SwmToken> to provide access to the indexed cron workflow data.

```go
func (f *cronWorkflowInformer) Lister() v1alpha1.CronWorkflowLister {
	return v1alpha1.NewCronWorkflowLister(f.Informer().GetIndexer())
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/listers/workflow/v1alpha1/workflowtemplate.go" line="28">

---

The <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflowtemplate.go" pos="28:2:2" line-data="// NewWorkflowTemplateLister returns a new WorkflowTemplateLister.">`NewWorkflowTemplateLister`</SwmToken> function initializes a new <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflowtemplate.go" pos="30:4:4" line-data="	return &amp;workflowTemplateLister{indexer: indexer}">`workflowTemplateLister`</SwmToken> with the provided indexer.

```go
// NewWorkflowTemplateLister returns a new WorkflowTemplateLister.
func NewWorkflowTemplateLister(indexer cache.Indexer) WorkflowTemplateLister {
	return &workflowTemplateLister{indexer: indexer}
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/informers/externalversions/workflow/v1alpha1/workflowtemplate.go" line="72">

---

<SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflowtemplate.go" pos="73:5:5" line-data="	return v1alpha1.NewWorkflowTemplateLister(f.Informer().GetIndexer())">`NewWorkflowTemplateLister`</SwmToken> is used within the <SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflowtemplate.go" pos="72:9:9" line-data="func (f *workflowTemplateInformer) Lister() v1alpha1.WorkflowTemplateLister {">`Lister`</SwmToken> function of <SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflowtemplate.go" pos="72:6:6" line-data="func (f *workflowTemplateInformer) Lister() v1alpha1.WorkflowTemplateLister {">`workflowTemplateInformer`</SwmToken> to provide access to the indexed workflow template data.

```go
func (f *workflowTemplateInformer) Lister() v1alpha1.WorkflowTemplateLister {
	return v1alpha1.NewWorkflowTemplateLister(f.Informer().GetIndexer())
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/listers/workflow/v1alpha1/workflowtaskset.go" line="28">

---

The <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflowtaskset.go" pos="28:2:2" line-data="// NewWorkflowTaskSetLister returns a new WorkflowTaskSetLister.">`NewWorkflowTaskSetLister`</SwmToken> function initializes a new <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflowtaskset.go" pos="30:4:4" line-data="	return &amp;workflowTaskSetLister{indexer: indexer}">`workflowTaskSetLister`</SwmToken> with the provided indexer.

```go
// NewWorkflowTaskSetLister returns a new WorkflowTaskSetLister.
func NewWorkflowTaskSetLister(indexer cache.Indexer) WorkflowTaskSetLister {
	return &workflowTaskSetLister{indexer: indexer}
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/informers/externalversions/workflow/v1alpha1/workflowtaskset.go" line="72">

---

<SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflowtaskset.go" pos="73:5:5" line-data="	return v1alpha1.NewWorkflowTaskSetLister(f.Informer().GetIndexer())">`NewWorkflowTaskSetLister`</SwmToken> is used within the <SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflowtaskset.go" pos="72:9:9" line-data="func (f *workflowTaskSetInformer) Lister() v1alpha1.WorkflowTaskSetLister {">`Lister`</SwmToken> function of <SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflowtaskset.go" pos="72:6:6" line-data="func (f *workflowTaskSetInformer) Lister() v1alpha1.WorkflowTaskSetLister {">`workflowTaskSetInformer`</SwmToken> to provide access to the indexed workflow task set data.

```go
func (f *workflowTaskSetInformer) Lister() v1alpha1.WorkflowTaskSetLister {
	return v1alpha1.NewWorkflowTaskSetLister(f.Informer().GetIndexer())
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/listers/workflow/v1alpha1/workflowtaskresult.go" line="28">

---

The <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflowtaskresult.go" pos="28:2:2" line-data="// NewWorkflowTaskResultLister returns a new WorkflowTaskResultLister.">`NewWorkflowTaskResultLister`</SwmToken> function initializes a new <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflowtaskresult.go" pos="30:4:4" line-data="	return &amp;workflowTaskResultLister{indexer: indexer}">`workflowTaskResultLister`</SwmToken> with the provided indexer.

```go
// NewWorkflowTaskResultLister returns a new WorkflowTaskResultLister.
func NewWorkflowTaskResultLister(indexer cache.Indexer) WorkflowTaskResultLister {
	return &workflowTaskResultLister{indexer: indexer}
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/informers/externalversions/workflow/v1alpha1/workflowtaskresult.go" line="72">

---

<SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflowtaskresult.go" pos="73:5:5" line-data="	return v1alpha1.NewWorkflowTaskResultLister(f.Informer().GetIndexer())">`NewWorkflowTaskResultLister`</SwmToken> is used within the <SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflowtaskresult.go" pos="72:9:9" line-data="func (f *workflowTaskResultInformer) Lister() v1alpha1.WorkflowTaskResultLister {">`Lister`</SwmToken> function of <SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflowtaskresult.go" pos="72:6:6" line-data="func (f *workflowTaskResultInformer) Lister() v1alpha1.WorkflowTaskResultLister {">`workflowTaskResultInformer`</SwmToken> to provide access to the indexed workflow task result data.

```go
func (f *workflowTaskResultInformer) Lister() v1alpha1.WorkflowTaskResultLister {
	return v1alpha1.NewWorkflowTaskResultLister(f.Informer().GetIndexer())
}
```

---

</SwmSnippet>

# Lister Endpoints

Lister endpoints provide methods to list and retrieve workflow objects. The primary methods are `List` and <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflow.go" pos="73:2:2" line-data="// Get retrieves the Workflow from the indexer for a given namespace and name.">`Get`</SwmToken>.

## List

The `List` function in the <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflow.go" pos="30:4:4" line-data="	return &amp;workflowLister{indexer: indexer}">`workflowLister`</SwmToken> struct lists all workflows in the indexer. It uses the <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflow.go" pos="35:5:7" line-data="	err = cache.ListAll(s.indexer, selector, func(m interface{}) {">`cache.ListAll`</SwmToken> function to retrieve the workflows based on the provided selector and appends them to the return slice.

<SwmSnippet path="/pkg/client/listers/workflow/v1alpha1/workflow.go" line="33">

---

The `List` function retrieves all workflows from the indexer using the <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflow.go" pos="35:5:7" line-data="	err = cache.ListAll(s.indexer, selector, func(m interface{}) {">`cache.ListAll`</SwmToken> function.

```go
// List lists all Workflows in the indexer.
func (s *workflowLister) List(selector labels.Selector) (ret []*v1alpha1.Workflow, err error) {
	err = cache.ListAll(s.indexer, selector, func(m interface{}) {
		ret = append(ret, m.(*v1alpha1.Workflow))
	})
	return ret, err
}
```

---

</SwmSnippet>

## Get

The <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflow.go" pos="73:2:2" line-data="// Get retrieves the Workflow from the indexer for a given namespace and name.">`Get`</SwmToken> function in the <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflow.go" pos="74:5:5" line-data="func (s workflowNamespaceLister) Get(name string) (*v1alpha1.Workflow, error) {">`workflowNamespaceLister`</SwmToken> struct retrieves a workflow from the indexer for a given namespace and name. It uses the <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflow.go" pos="29:6:8" line-data="func NewWorkflowLister(indexer cache.Indexer) WorkflowLister {">`cache.Indexer`</SwmToken>'s <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflow.go" pos="75:15:15" line-data="	obj, exists, err := s.indexer.GetByKey(s.namespace + &quot;/&quot; + name)">`GetByKey`</SwmToken> method to fetch the workflow and handles errors and non-existence cases.

<SwmSnippet path="/pkg/client/listers/workflow/v1alpha1/workflow.go" line="73">

---

The <SwmToken path="pkg/client/listers/workflow/v1alpha1/workflow.go" pos="73:2:2" line-data="// Get retrieves the Workflow from the indexer for a given namespace and name.">`Get`</SwmToken> function retrieves a workflow from the indexer using the `cache.Indexer.GetByKey` method and handles errors and non-existence cases.

```go
// Get retrieves the Workflow from the indexer for a given namespace and name.
func (s workflowNamespaceLister) Get(name string) (*v1alpha1.Workflow, error) {
	obj, exists, err := s.indexer.GetByKey(s.namespace + "/" + name)
	if err != nil {
		return nil, err
	}
	if !exists {
		return nil, errors.NewNotFound(v1alpha1.Resource("workflow"), name)
	}
	return obj.(*v1alpha1.Workflow), nil
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
