---
title: Clientset in Argo Workflows
---
# What is Clientset in Client

Clientset contains the clients for different API groups. Each group has exactly one version included in a Clientset. It is used to interact with the Argo Workflows API, providing methods to access different versions of the API.

<SwmSnippet path="/pkg/client/clientset/versioned/clientset.go" line="19">

---

## Clientset Structure

The <SwmToken path="pkg/client/clientset/versioned/clientset.go" pos="19:2:2" line-data="// Clientset contains the clients for groups. Each group has exactly one">`Clientset`</SwmToken> struct contains clients for different API groups, including a <SwmToken path="pkg/client/clientset/versioned/clientset.go" pos="22:4:4" line-data="	*discovery.DiscoveryClient">`DiscoveryClient`</SwmToken> and an <SwmToken path="pkg/client/clientset/versioned/clientset.go" pos="23:6:6" line-data="	argoprojV1alpha1 *argoprojv1alpha1.ArgoprojV1alpha1Client">`ArgoprojV1alpha1Client`</SwmToken>.

```go
// Clientset contains the clients for groups. Each group has exactly one
// version included in a Clientset.
type Clientset struct {
	*discovery.DiscoveryClient
	argoprojV1alpha1 *argoprojv1alpha1.ArgoprojV1alpha1Client
}
```

---

</SwmSnippet>

The <SwmToken path="pkg/client/clientset/versioned/clientset.go" pos="19:2:2" line-data="// Clientset contains the clients for groups. Each group has exactly one">`Clientset`</SwmToken> struct includes a <SwmToken path="pkg/client/clientset/versioned/clientset.go" pos="22:4:4" line-data="	*discovery.DiscoveryClient">`DiscoveryClient`</SwmToken> for discovering API resources and an <SwmToken path="pkg/client/clientset/versioned/clientset.go" pos="23:6:6" line-data="	argoprojV1alpha1 *argoprojv1alpha1.ArgoprojV1alpha1Client">`ArgoprojV1alpha1Client`</SwmToken> for interacting with the <SwmToken path="pkg/client/clientset/versioned/typed/workflow/v1alpha1/clusterworkflowtemplate.go" pos="49:34:34" line-data="func (c *clusterWorkflowTemplates) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.ClusterWorkflowTemplate, err error) {">`v1alpha1`</SwmToken> version of the Argo Workflows API.

## Fake Clientset for Testing

The fake <SwmToken path="pkg/client/clientset/versioned/clientset.go" pos="19:2:2" line-data="// Clientset contains the clients for groups. Each group has exactly one">`Clientset`</SwmToken> struct is used for testing purposes, allowing the simulation of API interactions without requiring a real Kubernetes cluster.

<SwmSnippet path="/pkg/client/clientset/versioned/fake/clientset_generated.go" line="44">

---

The fake <SwmToken path="pkg/client/clientset/versioned/fake/clientset_generated.go" pos="44:2:2" line-data="// Clientset implements clientset.Interface. Meant to be embedded into a">`Clientset`</SwmToken> struct is designed to be embedded into a struct to get a default implementation, making it easier to fake out just the method you want to test.

```go
// Clientset implements clientset.Interface. Meant to be embedded into a
// struct to get a default implementation. This makes faking out just the method
// you want to test easier.
type Clientset struct {
	testing.Fake
	discovery *fakediscovery.FakeDiscovery
	tracker   testing.ObjectTracker
}
```

---

</SwmSnippet>

## Creating a Fake Clientset

The <SwmToken path="pkg/client/clientset/versioned/fake/clientset_generated.go" pos="16:2:2" line-data="// NewSimpleClientset returns a clientset that will respond with the provided objects.">`NewSimpleClientset`</SwmToken> function returns a fake <SwmToken path="pkg/client/clientset/versioned/clientset.go" pos="19:2:2" line-data="// Clientset contains the clients for groups. Each group has exactly one">`Clientset`</SwmToken> that responds with provided objects, useful for unit tests.

<SwmSnippet path="/pkg/client/clientset/versioned/fake/clientset_generated.go" line="16">

---

The <SwmToken path="pkg/client/clientset/versioned/fake/clientset_generated.go" pos="16:2:2" line-data="// NewSimpleClientset returns a clientset that will respond with the provided objects.">`NewSimpleClientset`</SwmToken> function is backed by a simple object tracker that processes creates, updates, and deletions <SwmToken path="pkg/client/clientset/versioned/fake/clientset_generated.go" pos="17:33:35" line-data="// It&#39;s backed by a very simple object tracker that processes creates, updates and deletions as-is,">`as-is`</SwmToken>, without applying any validations <SwmToken path="pkg/client/clientset/versioned/fake/clientset_generated.go" pos="18:10:12" line-data="// without applying any validations and/or defaults. It shouldn&#39;t be considered a replacement">`and/or`</SwmToken> defaults.

```go
// NewSimpleClientset returns a clientset that will respond with the provided objects.
// It's backed by a very simple object tracker that processes creates, updates and deletions as-is,
// without applying any validations and/or defaults. It shouldn't be considered a replacement
// for a real clientset and is mostly useful in simple unit tests.
func NewSimpleClientset(objects ...runtime.Object) *Clientset {
	o := testing.NewObjectTracker(scheme, codecs.UniversalDecoder())
	for _, obj := range objects {
		if err := o.Add(obj); err != nil {
			panic(err)
		}
	}

	cs := &Clientset{tracker: o}
	cs.discovery = &fakediscovery.FakeDiscovery{Fake: &cs.Fake}
	cs.AddReactor("*", "*", testing.ObjectReaction(o))
	cs.AddWatchReactor("*", func(action testing.Action) (handled bool, ret watch.Interface, err error) {
		gvr := action.GetResource()
		ns := action.GetNamespace()
		watch, err := o.Watch(gvr, ns)
		if err != nil {
			return false, nil, err
```

---

</SwmSnippet>

## Clientset Endpoints

Clientset provides various endpoints to interact with the Argo Workflows API.

### Get

The <SwmToken path="pkg/client/clientset/versioned/typed/workflow/v1alpha1/clusterworkflowtemplate.go" pos="48:2:2" line-data="// Get takes name of the clusterWorkflowTemplate, and returns the corresponding clusterWorkflowTemplate object, and an error if there is any.">`Get`</SwmToken> method retrieves a specific <SwmToken path="pkg/client/clientset/versioned/typed/workflow/v1alpha1/clusterworkflowtemplate.go" pos="49:36:36" line-data="func (c *clusterWorkflowTemplates) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.ClusterWorkflowTemplate, err error) {">`ClusterWorkflowTemplate`</SwmToken> by its name. It constructs a GET request to the <SwmToken path="pkg/client/clientset/versioned/typed/workflow/v1alpha1/clusterworkflowtemplate.go" pos="52:4:4" line-data="		Resource(&quot;clusterworkflowtemplates&quot;).">`clusterworkflowtemplates`</SwmToken> resource, appending the name and options as query parameters. The result is then decoded into a <SwmToken path="pkg/client/clientset/versioned/typed/workflow/v1alpha1/clusterworkflowtemplate.go" pos="49:36:36" line-data="func (c *clusterWorkflowTemplates) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.ClusterWorkflowTemplate, err error) {">`ClusterWorkflowTemplate`</SwmToken> object.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/workflow/v1alpha1/clusterworkflowtemplate.go" line="48">

---

The <SwmToken path="pkg/client/clientset/versioned/typed/workflow/v1alpha1/clusterworkflowtemplate.go" pos="48:2:2" line-data="// Get takes name of the clusterWorkflowTemplate, and returns the corresponding clusterWorkflowTemplate object, and an error if there is any.">`Get`</SwmToken> method constructs a GET request to retrieve a specific <SwmToken path="pkg/client/clientset/versioned/typed/workflow/v1alpha1/clusterworkflowtemplate.go" pos="49:36:36" line-data="func (c *clusterWorkflowTemplates) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.ClusterWorkflowTemplate, err error) {">`ClusterWorkflowTemplate`</SwmToken>.

```go
// Get takes name of the clusterWorkflowTemplate, and returns the corresponding clusterWorkflowTemplate object, and an error if there is any.
func (c *clusterWorkflowTemplates) Get(ctx context.Context, name string, options v1.GetOptions) (result *v1alpha1.ClusterWorkflowTemplate, err error) {
	result = &v1alpha1.ClusterWorkflowTemplate{}
	err = c.client.Get().
		Resource("clusterworkflowtemplates").
		Name(name).
		VersionedParams(&options, scheme.ParameterCodec).
		Do(ctx).
		Into(result)
	return
}
```

---

</SwmSnippet>

### List

The `List` method retrieves a list of <SwmToken path="pkg/client/clientset/versioned/typed/workflow/v1alpha1/clusterworkflowtemplate.go" pos="60:25:25" line-data="// List takes label and field selectors, and returns the list of ClusterWorkflowTemplates that match those selectors.">`ClusterWorkflowTemplates`</SwmToken> that match the provided label and field selectors. It constructs a GET request to the <SwmToken path="pkg/client/clientset/versioned/typed/workflow/v1alpha1/clusterworkflowtemplate.go" pos="52:4:4" line-data="		Resource(&quot;clusterworkflowtemplates&quot;).">`clusterworkflowtemplates`</SwmToken> resource, including the selectors and timeout as query parameters. The result is decoded into a <SwmToken path="pkg/client/clientset/versioned/typed/workflow/v1alpha1/clusterworkflowtemplate.go" pos="61:31:31" line-data="func (c *clusterWorkflowTemplates) List(ctx context.Context, opts v1.ListOptions) (result *v1alpha1.ClusterWorkflowTemplateList, err error) {">`ClusterWorkflowTemplateList`</SwmToken> object.

<SwmSnippet path="/pkg/client/clientset/versioned/typed/workflow/v1alpha1/clusterworkflowtemplate.go" line="60">

---

The `List` method constructs a GET request to retrieve a list of <SwmToken path="pkg/client/clientset/versioned/typed/workflow/v1alpha1/clusterworkflowtemplate.go" pos="60:25:25" line-data="// List takes label and field selectors, and returns the list of ClusterWorkflowTemplates that match those selectors.">`ClusterWorkflowTemplates`</SwmToken>.

```go
// List takes label and field selectors, and returns the list of ClusterWorkflowTemplates that match those selectors.
func (c *clusterWorkflowTemplates) List(ctx context.Context, opts v1.ListOptions) (result *v1alpha1.ClusterWorkflowTemplateList, err error) {
	var timeout time.Duration
	if opts.TimeoutSeconds != nil {
		timeout = time.Duration(*opts.TimeoutSeconds) * time.Second
	}
	result = &v1alpha1.ClusterWorkflowTemplateList{}
	err = c.client.Get().
		Resource("clusterworkflowtemplates").
		VersionedParams(&opts, scheme.ParameterCodec).
		Timeout(timeout).
		Do(ctx).
		Into(result)
	return
}
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](https://app.swimm.io/)</sup></SwmMeta>
