---
title: Creating a Workflow
---
In this document, we will explain the process of creating a workflow. The process involves constructing a POST request with the workflow data, sending it to the server, and handling the server's response.

The flow starts with creating a representation of the workflow and then constructing a POST request with this data. This request is sent to the server, which processes it and returns the created workflow's representation. The server's response is then handled to complete the creation process.

# Flow drill down

```mermaid
graph TD;
      6d3cd56d7ff2c0a0f50ec75910df92d3bba35e9824e44488daf0c42a8a3146f6(Create):::mainFlowStyle --> 3193f58216eaafc13f1f2fcaea8d8f034faac59713ffd7a7dfea7f86eca4f84a(Post):::mainFlowStyle

3193f58216eaafc13f1f2fcaea8d8f034faac59713ffd7a7dfea7f86eca4f84a(Post):::mainFlowStyle --> 62d60fefad022c005b2fc4b9d21a23b27e33587e9bc3b0976e3bd5ffc2cab44e(do):::mainFlowStyle

62d60fefad022c005b2fc4b9d21a23b27e33587e9bc3b0976e3bd5ffc2cab44e(do):::mainFlowStyle --> c851f97860e9a6bfa58443988546f4495496430e2ba7bbf204959a5e87d009f3(url):::mainFlowStyle

subgraph utilflattenflattengo["util/flatten/flatten.go"]
c851f97860e9a6bfa58443988546f4495496430e2ba7bbf204959a5e87d009f3(url):::mainFlowStyle --> 472f5adb55d157edddc63d62fcb73cefc54efccc4d5d60c2794807335a70ee54(Flatten):::mainFlowStyle
end

subgraph utilflattenflattengo["util/flatten/flatten.go"]
472f5adb55d157edddc63d62fcb73cefc54efccc4d5d60c2794807335a70ee54(Flatten):::mainFlowStyle --> cc0909409e21db09338d11a894e991c37e97797ba5bb7137a95d7d43bf31f668(flattenWithPrefix):::mainFlowStyle
end


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9
```

<SwmSnippet path="/pkg/client/clientset/versioned/typed/workflow/v1alpha1/workflow.go" line="95">

---

## Creating the Workflow

The <SwmToken path="pkg/client/clientset/versioned/typed/workflow/v1alpha1/workflow.go" pos="95:2:2" line-data="// Create takes the representation of a workflow and creates it.  Returns the server&#39;s representation of the workflow, and an error, if there is any.">`Create`</SwmToken> function is responsible for taking the representation of a workflow and creating it on the server. It constructs a POST request with the workflow data and sends it to the server. The server's response, which includes the created workflow's representation, is then returned.

```go
// Create takes the representation of a workflow and creates it.  Returns the server's representation of the workflow, and an error, if there is any.
func (c *workflows) Create(ctx context.Context, workflow *v1alpha1.Workflow, opts v1.CreateOptions) (result *v1alpha1.Workflow, err error) {
	result = &v1alpha1.Workflow{}
	err = c.client.Post().
		Namespace(c.ns).
		Resource("workflows").
		VersionedParams(&opts, scheme.ParameterCodec).
		Body(workflow).
		Do(ctx).
		Into(result)
	return
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apiclient/http1/facade.go" line="44">

---

## Posting the Workflow

The <SwmToken path="pkg/apiclient/http1/facade.go" pos="44:8:8" line-data="func (h Facade) Post(ctx context.Context, in, out interface{}, path string) error {">`Post`</SwmToken> function is used to send a POST request to a specified path. It calls the <SwmToken path="pkg/apiclient/http1/facade.go" pos="45:5:5" line-data="	return h.do(ctx, in, out, &quot;POST&quot;, path)">`do`</SwmToken> function with the method set to 'POST'.

```go
func (h Facade) Post(ctx context.Context, in, out interface{}, path string) error {
	return h.do(ctx, in, out, "POST", path)
}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apiclient/http1/facade.go" line="92">

---

### Executing the POST Request

The <SwmToken path="pkg/apiclient/http1/facade.go" pos="92:8:8" line-data="func (h Facade) do(ctx context.Context, in interface{}, out interface{}, method string, path string) error {">`do`</SwmToken> function handles the execution of the HTTP request. It serializes the input data to JSON, constructs the URL, and sets up the HTTP request with the appropriate headers. It then sends the request using an HTTP client and processes the response.

```go
func (h Facade) do(ctx context.Context, in interface{}, out interface{}, method string, path string) error {
	var data []byte
	if method != "GET" {
		var err error
		data, err = json.Marshal(in)
		if err != nil {
			return err
		}
	}
	u, err := h.url(method, path, in)
	if err != nil {
		return err
	}
	req, err := http.NewRequestWithContext(ctx, method, u.String(), bytes.NewReader(data))
	if err != nil {
		return err
	}
	headers, err := parseHeaders(h.headers)
	if err != nil {
		return err
	}
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apiclient/http1/facade.go" line="143">

---

### Constructing the URL

The <SwmToken path="pkg/apiclient/http1/facade.go" pos="143:8:8" line-data="func (h Facade) url(method, path string, in interface{}) (*url.URL, error) {">`url`</SwmToken> function constructs the URL for the HTTP request. It flattens the input data into a map of query parameters and replaces placeholders in the path with actual values. It then constructs the final URL with the query parameters.

```go
func (h Facade) url(method, path string, in interface{}) (*url.URL, error) {
	query := url.Values{}
	for s, v := range flatten.Flatten(in) {
		x := "{" + s + "}"
		if strings.Contains(path, x) {
			path = strings.Replace(path, x, v, 1)
		} else if method == "GET" {
			query.Set(s, v)
		}
	}
	// remove any that were not provided
	path = regexp.MustCompile("{[^}]*}").ReplaceAllString(path, "")
	return url.Parse(h.baseUrl + path + "?" + query.Encode())
}
```

---

</SwmSnippet>

<SwmSnippet path="/util/flatten/flatten.go" line="29">

---

## Flattening the Input Data

The <SwmToken path="util/flatten/flatten.go" pos="29:2:2" line-data="// Flatten converts a struct into a map[string]string using dot-notation.">`Flatten`</SwmToken> function converts a struct into a map of strings using <SwmToken path="util/flatten/flatten.go" pos="29:22:24" line-data="// Flatten converts a struct into a map[string]string using dot-notation.">`dot-notation`</SwmToken>. This is used to create query parameters from the input data.

```go
// Flatten converts a struct into a map[string]string using dot-notation.
// E.g. listOptions.continue="10"
func Flatten(in interface{}) map[string]string {
	out := make(map[string]string)
	flattenWithPrefix(toMap(in), out, "")
	return out
}
```

---

</SwmSnippet>

<SwmSnippet path="/util/flatten/flatten.go" line="15">

---

### Flattening with Prefix

The <SwmToken path="util/flatten/flatten.go" pos="15:2:2" line-data="func flattenWithPrefix(in map[string]interface{}, out map[string]string, prefix string) {">`flattenWithPrefix`</SwmToken> function is a helper function used by <SwmToken path="pkg/apiclient/http1/facade.go" pos="145:14:14" line-data="	for s, v := range flatten.Flatten(in) {">`Flatten`</SwmToken> to recursively flatten nested maps. It adds a prefix to the keys to maintain the <SwmToken path="util/flatten/flatten.go" pos="29:22:24" line-data="// Flatten converts a struct into a map[string]string using dot-notation.">`dot-notation`</SwmToken> structure.

```go
func flattenWithPrefix(in map[string]interface{}, out map[string]string, prefix string) {
	for k, v := range in {
		if v == nil {
			continue
		}
		switch reflect.TypeOf(v).Kind() {
		case reflect.Map:
			flattenWithPrefix(toMap(v), out, prefix+k+".")
		default:
			out[prefix+k] = fmt.Sprintf("%v", v)
		}
	}
}
```

---

</SwmSnippet>

# Where is this flow used?

This flow is used multiple times in the codebase as represented in the following diagram:

(Note - these are only some of the entry points of this flow)

```mermaid
graph TD;
      subgraph workflowexecutor["workflow/executor"]
0cd46957c714951f5f42bc65b9bfe7ad46c69811200a24fd8d20d0e78ea13d4e(WorkflowLogs):::rootsStyle --> dfc8b1a9085ee34648918919002330b84c096100a5d33d345ecafa2cf43f6b46(Wait)
end

subgraph workflowexecutor["workflow/executor"]
dfc8b1a9085ee34648918919002330b84c096100a5d33d345ecafa2cf43f6b46(Wait) --> 375605047891e3c417d24173ea49f7739114c907c4ec3728820d78c23e408a47(monitorProgress)
end

subgraph workflowexecutor["workflow/executor"]
375605047891e3c417d24173ea49f7739114c907c4ec3728820d78c23e408a47(monitorProgress) --> 973b83ae73ff805c354808346380500f59711b9f52b11a26537c8cf25fa296ef(reportResult)
end

subgraph workflowexecutor["workflow/executor"]
973b83ae73ff805c354808346380500f59711b9f52b11a26537c8cf25fa296ef(reportResult) --> 1d8b41a5f2780223f15889b838ad832279e7f11945bcafc5b79b5734f8e6ad0f(upsertTaskResult)
end

subgraph workflowexecutor["workflow/executor"]
1d8b41a5f2780223f15889b838ad832279e7f11945bcafc5b79b5734f8e6ad0f(upsertTaskResult) --> 41759cea2956f38d54c988938410325fd8c8bcc90d89e8f8f6914f3dfe8bd060(createTaskResult)
end

41759cea2956f38d54c988938410325fd8c8bcc90d89e8f8f6914f3dfe8bd060(createTaskResult) --> 6d3cd56d7ff2c0a0f50ec75910df92d3bba35e9824e44488daf0c42a8a3146f6(Create):::mainFlowStyle

subgraph serverevent["server/event"]
9a92bef37349d0e1c6d50c1c571af7a786363d550888bf19455ef8943ed6b48a(ReceiveEvent):::rootsStyle --> 77dce874ef76a82ae7a8463da070b9b87c5d7d19dcca895f6ed1911b5084002c(Dispatch)
end

subgraph serverevent["server/event"]
77dce874ef76a82ae7a8463da070b9b87c5d7d19dcca895f6ed1911b5084002c(Dispatch) --> feddfb78cfbcedcf7975a0b292c796eaaaeeeb6b95431bef6b7b963fc790c720(dispatch)
end

subgraph serverevent["server/event"]
feddfb78cfbcedcf7975a0b292c796eaaaeeeb6b95431bef6b7b963fc790c720(dispatch) --> 342e9be43e716fffd3fca0f76980b54ce2265f66eccb4655575ca573bf276c9d(Run)
end

subgraph workflowexecutor["workflow/executor"]
342e9be43e716fffd3fca0f76980b54ce2265f66eccb4655575ca573bf276c9d(Run) --> dfc8b1a9085ee34648918919002330b84c096100a5d33d345ecafa2cf43f6b46(Wait)
end

subgraph hackapiswagger["hack/api/swagger"]
227eaee48f790cb276fab7c3bb5c4aed07dc34a153c81931559b3ec413b1cb32(main):::rootsStyle --> 52208eac7c0bcaca66e943084dff10f4c38d5375299a688e1548aa70c502587d(kubeifySwagger)
end

52208eac7c0bcaca66e943084dff10f4c38d5375299a688e1548aa70c502587d(kubeifySwagger) --> 6d3cd56d7ff2c0a0f50ec75910df92d3bba35e9824e44488daf0c42a8a3146f6(Create):::mainFlowStyle

subgraph serverworkflowworkflowservergo["server/workflow/workflow_server.go"]
8cb50919d2e74383376a1d3a4429d0f6248d7478d162fb4e5669a52f08cf5a79(NewWorkflowServiceClient):::rootsStyle --> c13a058e437520df8e9237aa457fa1b1308ed9b06e3765222df3de76873dae09(NewWorkflowServer)
end

subgraph serverauth["server/auth"]
c13a058e437520df8e9237aa457fa1b1308ed9b06e3765222df3de76873dae09(NewWorkflowServer) --> 85c74d53af7059ac195bd0a57918f577a57700ab071e38a539f8e0d792c26961(New)
end

subgraph serverauth["server/auth"]
85c74d53af7059ac195bd0a57918f577a57700ab071e38a539f8e0d792c26961(New) --> 3ad4a8ea8b09a394dfe0b59c7d4acf8f96ece172eb229552c53c83d50c996812(newSso)
end

3ad4a8ea8b09a394dfe0b59c7d4acf8f96ece172eb229552c53c83d50c996812(newSso) --> 6d3cd56d7ff2c0a0f50ec75910df92d3bba35e9824e44488daf0c42a8a3146f6(Create):::mainFlowStyle

subgraph serverauth["server/auth"]
5c4ed23a3e8e7cecb78ad3ee142a12ea89123dbb9dad7682b19049d3f20e46fa(Add):::rootsStyle --> 85c74d53af7059ac195bd0a57918f577a57700ab071e38a539f8e0d792c26961(New)
end


      classDef mainFlowStyle color:#000000,fill:#7CB9F4
classDef rootsStyle color:#000000,fill:#00FFF4
classDef Style1 color:#000000,fill:#00FFAA
classDef Style2 color:#000000,fill:#FFFF00
classDef Style3 color:#000000,fill:#AA7CB9
```

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
