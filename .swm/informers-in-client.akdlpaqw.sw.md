---
title: Informers in Client
---
# What are Informers in Client

Informers provide access to a shared informer and lister for various Kubernetes resources. They are responsible for constructing and managing shared index informers, which watch and list resources from the Kubernetes API server.

<SwmSnippet path="/pkg/client/informers/externalversions/generic.go" line="25">

---

# Informer Method

The <SwmToken path="pkg/client/informers/externalversions/generic.go" pos="25:2:2" line-data="// Informer returns the SharedIndexInformer.">`Informer`</SwmToken> method returns the <SwmToken path="pkg/client/informers/externalversions/generic.go" pos="25:8:8" line-data="// Informer returns the SharedIndexInformer.">`SharedIndexInformer`</SwmToken> instance, which is used to manage the lifecycle of the informer.

```go
// Informer returns the SharedIndexInformer.
func (f *genericInformer) Informer() cache.SharedIndexInformer {
	return f.informer
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/informers/externalversions/factory.go" line="94">

---

# Start Method

The <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="94:2:2" line-data="// Start initializes all requested informers.">`Start`</SwmToken> method initializes all requested informers and starts them by calling their <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="101:5:5" line-data="			go informer.Run(stopCh)">`Run`</SwmToken> method.

```go
// Start initializes all requested informers.
func (f *sharedInformerFactory) Start(stopCh <-chan struct{}) {
	f.lock.Lock()
	defer f.lock.Unlock()

	for informerType, informer := range f.informers {
		if !f.startedInformers[informerType] {
			go informer.Run(stopCh)
			f.startedInformers[informerType] = true
		}
	}
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/informers/externalversions/factory.go" line="129">

---

# <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="131:9:9" line-data="func (f *sharedInformerFactory) InformerFor(obj runtime.Object, newFunc internalinterfaces.NewInformerFunc) cache.SharedIndexInformer {">`InformerFor`</SwmToken> Method

The <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="131:9:9" line-data="func (f *sharedInformerFactory) InformerFor(obj runtime.Object, newFunc internalinterfaces.NewInformerFunc) cache.SharedIndexInformer {">`InformerFor`</SwmToken> method returns the <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="129:8:8" line-data="// InternalInformerFor returns the SharedIndexInformer for obj using an internal">`SharedIndexInformer`</SwmToken> for a given object type, ensuring that the informer is created and started if it does not already exist.

```go
// InternalInformerFor returns the SharedIndexInformer for obj using an internal
// client.
func (f *sharedInformerFactory) InformerFor(obj runtime.Object, newFunc internalinterfaces.NewInformerFunc) cache.SharedIndexInformer {
	f.lock.Lock()
	defer f.lock.Unlock()

	informerType := reflect.TypeOf(obj)
	informer, exists := f.informers[informerType]
	if exists {
		return informer
	}

	resyncPeriod, exists := f.customResync[informerType]
	if !exists {
		resyncPeriod = f.defaultResync
	}

	informer = newFunc(f.client, resyncPeriod)
	f.informers[informerType] = informer

	return informer
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/informers/externalversions/workflow/v1alpha1/workflow.go" line="32">

---

# <SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflow.go" pos="32:2:2" line-data="// NewWorkflowInformer constructs a new informer for Workflow type.">`NewWorkflowInformer`</SwmToken> Function

The <SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflow.go" pos="32:2:2" line-data="// NewWorkflowInformer constructs a new informer for Workflow type.">`NewWorkflowInformer`</SwmToken> function constructs a new informer for the Workflow type, reducing memory footprint and the number of connections to the server.

```go
// NewWorkflowInformer constructs a new informer for Workflow type.
// Always prefer using an informer factory to get a shared informer instead of getting an independent
// one. This reduces memory footprint and number of connections to the server.
func NewWorkflowInformer(client versioned.Interface, namespace string, resyncPeriod time.Duration, indexers cache.Indexers) cache.SharedIndexInformer {
	return NewFilteredWorkflowInformer(client, namespace, resyncPeriod, indexers, nil)
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/informers/externalversions/workflow/v1alpha1/workflow.go" line="39">

---

# <SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflow.go" pos="39:2:2" line-data="// NewFilteredWorkflowInformer constructs a new informer for Workflow type.">`NewFilteredWorkflowInformer`</SwmToken> Function

The <SwmToken path="pkg/client/informers/externalversions/workflow/v1alpha1/workflow.go" pos="39:2:2" line-data="// NewFilteredWorkflowInformer constructs a new informer for Workflow type.">`NewFilteredWorkflowInformer`</SwmToken> function constructs a new informer for the Workflow type, reducing memory footprint and the number of connections to the server.

```go
// NewFilteredWorkflowInformer constructs a new informer for Workflow type.
// Always prefer using an informer factory to get a shared informer instead of getting an independent
// one. This reduces memory footprint and number of connections to the server.
func NewFilteredWorkflowInformer(client versioned.Interface, namespace string, resyncPeriod time.Duration, indexers cache.Indexers, tweakListOptions internalinterfaces.TweakListOptionsFunc) cache.SharedIndexInformer {
	return cache.NewSharedIndexInformer(
		&cache.ListWatch{
			ListFunc: func(options v1.ListOptions) (runtime.Object, error) {
				if tweakListOptions != nil {
					tweakListOptions(&options)
				}
				return client.ArgoprojV1alpha1().Workflows(namespace).List(context.TODO(), options)
			},
			WatchFunc: func(options v1.ListOptions) (watch.Interface, error) {
				if tweakListOptions != nil {
					tweakListOptions(&options)
				}
				return client.ArgoprojV1alpha1().Workflows(namespace).Watch(context.TODO(), options)
			},
		},
		&workflowv1alpha1.Workflow{},
		resyncPeriod,
```

---

</SwmSnippet>

# Informer Endpoints

Endpoints of Informers provide various functionalities to interact with informers.

<SwmSnippet path="/pkg/client/informers/externalversions/generic.go" line="35">

---

## <SwmToken path="pkg/client/informers/externalversions/generic.go" pos="35:2:2" line-data="// ForResource gives generic access to a shared informer of the matching type">`ForResource`</SwmToken>

The <SwmToken path="pkg/client/informers/externalversions/generic.go" pos="35:2:2" line-data="// ForResource gives generic access to a shared informer of the matching type">`ForResource`</SwmToken> function provides generic access to a shared informer of the matching type. It switches on the resource type and returns the appropriate informer. If no informer is found for the given resource, it returns an error.

```go
// ForResource gives generic access to a shared informer of the matching type
// TODO extend this to unknown resources with a client pool
func (f *sharedInformerFactory) ForResource(resource schema.GroupVersionResource) (GenericInformer, error) {
	switch resource {
	// Group=argoproj.io, Version=v1alpha1
	case v1alpha1.SchemeGroupVersion.WithResource("clusterworkflowtemplates"):
		return &genericInformer{resource: resource.GroupResource(), informer: f.Argoproj().V1alpha1().ClusterWorkflowTemplates().Informer()}, nil
	case v1alpha1.SchemeGroupVersion.WithResource("cronworkflows"):
		return &genericInformer{resource: resource.GroupResource(), informer: f.Argoproj().V1alpha1().CronWorkflows().Informer()}, nil
	case v1alpha1.SchemeGroupVersion.WithResource("workflows"):
		return &genericInformer{resource: resource.GroupResource(), informer: f.Argoproj().V1alpha1().Workflows().Informer()}, nil
	case v1alpha1.SchemeGroupVersion.WithResource("workflowartifactgctasks"):
		return &genericInformer{resource: resource.GroupResource(), informer: f.Argoproj().V1alpha1().WorkflowArtifactGCTasks().Informer()}, nil
	case v1alpha1.SchemeGroupVersion.WithResource("workfloweventbindings"):
		return &genericInformer{resource: resource.GroupResource(), informer: f.Argoproj().V1alpha1().WorkflowEventBindings().Informer()}, nil
	case v1alpha1.SchemeGroupVersion.WithResource("workflowtaskresults"):
		return &genericInformer{resource: resource.GroupResource(), informer: f.Argoproj().V1alpha1().WorkflowTaskResults().Informer()}, nil
	case v1alpha1.SchemeGroupVersion.WithResource("workflowtasksets"):
		return &genericInformer{resource: resource.GroupResource(), informer: f.Argoproj().V1alpha1().WorkflowTaskSets().Informer()}, nil
	case v1alpha1.SchemeGroupVersion.WithResource("workflowtemplates"):
		return &genericInformer{resource: resource.GroupResource(), informer: f.Argoproj().V1alpha1().WorkflowTemplates().Informer()}, nil
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/client/informers/externalversions/factory.go" line="129">

---

## <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="131:9:9" line-data="func (f *sharedInformerFactory) InformerFor(obj runtime.Object, newFunc internalinterfaces.NewInformerFunc) cache.SharedIndexInformer {">`InformerFor`</SwmToken>

The <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="131:9:9" line-data="func (f *sharedInformerFactory) InformerFor(obj runtime.Object, newFunc internalinterfaces.NewInformerFunc) cache.SharedIndexInformer {">`InformerFor`</SwmToken> method returns the <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="129:8:8" line-data="// InternalInformerFor returns the SharedIndexInformer for obj using an internal">`SharedIndexInformer`</SwmToken> for a given object type. It ensures that the informer is created and started if it does not already exist. This method locks the factory, checks if the informer already exists, and if not, creates a new one using the provided <SwmToken path="pkg/client/informers/externalversions/factory.go" pos="131:18:18" line-data="func (f *sharedInformerFactory) InformerFor(obj runtime.Object, newFunc internalinterfaces.NewInformerFunc) cache.SharedIndexInformer {">`newFunc`</SwmToken>.

```go
// InternalInformerFor returns the SharedIndexInformer for obj using an internal
// client.
func (f *sharedInformerFactory) InformerFor(obj runtime.Object, newFunc internalinterfaces.NewInformerFunc) cache.SharedIndexInformer {
	f.lock.Lock()
	defer f.lock.Unlock()

	informerType := reflect.TypeOf(obj)
	informer, exists := f.informers[informerType]
	if exists {
		return informer
	}

	resyncPeriod, exists := f.customResync[informerType]
	if !exists {
		resyncPeriod = f.defaultResync
	}

	informer = newFunc(f.client, resyncPeriod)
	f.informers[informerType] = informer

	return informer
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
