---
title: Exploring Eventsource in Apiclient
---
## Overview

Eventsource refers to the component responsible for managing event sources within the Apiclient package. It handles requests related to creating, updating, deleting, and listing event sources.

## <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="72:2:2" line-data="service EventSourceService {">`EventSourceService`</SwmToken>

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="72:2:2" line-data="service EventSourceService {">`EventSourceService`</SwmToken> provides RPC methods to interact with event sources, such as <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="74:3:3" line-data="  rpc CreateEventSource(CreateEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`CreateEventSource`</SwmToken>, <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="81:3:3" line-data="  rpc GetEventSource(GetEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`GetEventSource`</SwmToken>, and <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="85:3:3" line-data="  rpc DeleteEventSource(DeleteEventSourceRequest) returns (EventSourceDeletedResponse) {">`DeleteEventSource`</SwmToken>.

<SwmSnippet path="/pkg/apiclient/eventsource/eventsource.proto" line="72">

---

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="72:2:2" line-data="service EventSourceService {">`EventSourceService`</SwmToken> defines the RPC methods for managing event sources. Here is the definition of the service.

```protocol buffer
service EventSourceService {

  rpc CreateEventSource(CreateEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {
```

---

</SwmSnippet>

## <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="11:2:2" line-data="message CreateEventSourceRequest {">`CreateEventSourceRequest`</SwmToken>

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="11:2:2" line-data="message CreateEventSourceRequest {">`CreateEventSourceRequest`</SwmToken> message is used to structure the data for creating an event source.

<SwmSnippet path="/pkg/apiclient/eventsource/eventsource.proto" line="11">

---

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="11:2:2" line-data="message CreateEventSourceRequest {">`CreateEventSourceRequest`</SwmToken> message includes the namespace and the event source details.

```protocol buffer
message CreateEventSourceRequest {
  string namespace = 1;
  github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource eventSource = 2;
```

---

</SwmSnippet>

## <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="16:2:2" line-data="message GetEventSourceRequest {">`GetEventSourceRequest`</SwmToken>

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="16:2:2" line-data="message GetEventSourceRequest {">`GetEventSourceRequest`</SwmToken> message is used to structure the data for retrieving an event source.

<SwmSnippet path="/pkg/apiclient/eventsource/eventsource.proto" line="16">

---

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="16:2:2" line-data="message GetEventSourceRequest {">`GetEventSourceRequest`</SwmToken> message includes the name and namespace of the event source.

```protocol buffer
message GetEventSourceRequest {
  string name = 1;
  string namespace = 2;
```

---

</SwmSnippet>

## <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="64:2:2" line-data="message EventSourceWatchEvent {">`EventSourceWatchEvent`</SwmToken>

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="64:2:2" line-data="message EventSourceWatchEvent {">`EventSourceWatchEvent`</SwmToken> message is used to watch for changes in event sources.

<SwmSnippet path="/pkg/apiclient/eventsource/eventsource.proto" line="64">

---

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="64:2:2" line-data="message EventSourceWatchEvent {">`EventSourceWatchEvent`</SwmToken> message includes the type of event and the event source object.

```protocol buffer
message EventSourceWatchEvent {
  string type = 1;
  github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource object = 2;
```

---

</SwmSnippet>

## Main Functions

The main functions provided by the <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="72:2:2" line-data="service EventSourceService {">`EventSourceService`</SwmToken> include <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="74:3:3" line-data="  rpc CreateEventSource(CreateEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`CreateEventSource`</SwmToken> and <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="81:3:3" line-data="  rpc GetEventSource(GetEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`GetEventSource`</SwmToken>.

### <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="74:3:3" line-data="  rpc CreateEventSource(CreateEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`CreateEventSource`</SwmToken>

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="74:3:3" line-data="  rpc CreateEventSource(CreateEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`CreateEventSource`</SwmToken> function is used to create a new event source. It takes a <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="11:2:2" line-data="message CreateEventSourceRequest {">`CreateEventSourceRequest`</SwmToken> message that includes the namespace and the event source details.

<SwmSnippet path="/pkg/apiclient/eventsource/eventsource.proto" line="11">

---

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="11:2:2" line-data="message CreateEventSourceRequest {">`CreateEventSourceRequest`</SwmToken> message structure is shown here.

```protocol buffer
message CreateEventSourceRequest {
  string namespace = 1;
  github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource eventSource = 2;
}
```

---

</SwmSnippet>

### <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="81:3:3" line-data="  rpc GetEventSource(GetEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`GetEventSource`</SwmToken>

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="81:3:3" line-data="  rpc GetEventSource(GetEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`GetEventSource`</SwmToken> function retrieves an event source by its name and namespace. It uses the <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="16:2:2" line-data="message GetEventSourceRequest {">`GetEventSourceRequest`</SwmToken> message to structure the request data.

<SwmSnippet path="/pkg/apiclient/eventsource/eventsource.proto" line="16">

---

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="16:2:2" line-data="message GetEventSourceRequest {">`GetEventSourceRequest`</SwmToken> message structure is shown here.

```protocol buffer
message GetEventSourceRequest {
  string name = 1;
  string namespace = 2;
}
```

---

</SwmSnippet>

## Eventsource Endpoints

The Eventsource endpoints include <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="74:3:3" line-data="  rpc CreateEventSource(CreateEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`CreateEventSource`</SwmToken> and <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="81:3:3" line-data="  rpc GetEventSource(GetEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`GetEventSource`</SwmToken>.

### <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="74:3:3" line-data="  rpc CreateEventSource(CreateEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`CreateEventSource`</SwmToken>

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="74:3:3" line-data="  rpc CreateEventSource(CreateEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`CreateEventSource`</SwmToken> endpoint is used to create a new event source. It accepts a <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="11:2:2" line-data="message CreateEventSourceRequest {">`CreateEventSourceRequest`</SwmToken> message containing the namespace and event source details, and returns the created event source object. The HTTP method used is POST, and the URL pattern is <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="76:6:17" line-data="      post : &quot;/api/v1/event-sources/{namespace}&quot;">`/api/v1/event-sources/{namespace}`</SwmToken>.

<SwmSnippet path="/pkg/apiclient/eventsource/eventsource.proto" line="74">

---

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="74:3:3" line-data="  rpc CreateEventSource(CreateEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`CreateEventSource`</SwmToken> endpoint definition is shown here.

```protocol buffer
  rpc CreateEventSource(CreateEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {
    option (google.api.http) = {
      post : "/api/v1/event-sources/{namespace}"
      body : "*"
    };
  }
```

---

</SwmSnippet>

### <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="81:3:3" line-data="  rpc GetEventSource(GetEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`GetEventSource`</SwmToken>

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="81:3:3" line-data="  rpc GetEventSource(GetEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`GetEventSource`</SwmToken> endpoint is used to retrieve an event source by its name and namespace. It accepts a <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="16:2:2" line-data="message GetEventSourceRequest {">`GetEventSourceRequest`</SwmToken> message containing the name and namespace, and returns the corresponding event source object. The HTTP method used is GET, and the URL pattern is <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="82:16:31" line-data="    option (google.api.http).get = &quot;/api/v1/event-sources/{namespace}/{name}&quot;;">`/api/v1/event-sources/{namespace}/{name}`</SwmToken>.

<SwmSnippet path="/pkg/apiclient/eventsource/eventsource.proto" line="81">

---

The <SwmToken path="pkg/apiclient/eventsource/eventsource.proto" pos="81:3:3" line-data="  rpc GetEventSource(GetEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {">`GetEventSource`</SwmToken> endpoint definition is shown here.

```protocol buffer
  rpc GetEventSource(GetEventSourceRequest) returns (github.com.argoproj.argo_events.pkg.apis.eventsource.v1alpha1.EventSource) {
    option (google.api.http).get = "/api/v1/event-sources/{namespace}/{name}";
  }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
