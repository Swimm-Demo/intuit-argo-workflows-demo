---
title: Getting Started with Info Service
---
# Getting Started with Info Service

The <SwmToken path="pkg/apiclient/info/info.proto" pos="45:2:2" line-data="service InfoService {">`InfoService`</SwmToken> is a part of the `Apiclient` package and provides various information-related functionalities. This document will guide you through the main methods and endpoints of the <SwmToken path="pkg/apiclient/info/info.proto" pos="45:2:2" line-data="service InfoService {">`InfoService`</SwmToken>, including <SwmToken path="pkg/apiclient/info/info.proto" pos="46:3:3" line-data="  rpc GetInfo(GetInfoRequest) returns (InfoResponse) {">`GetInfo`</SwmToken>, <SwmToken path="pkg/apiclient/info/info.pb.go" pos="512:9:9" line-data="func (c *infoServiceClient) GetVersion(ctx context.Context, in *GetVersionRequest, opts ...grpc.CallOption) (*v1alpha1.Version, error) {">`GetVersion`</SwmToken>, <SwmToken path="pkg/apiclient/info/info.proto" pos="52:3:3" line-data="  rpc GetUserInfo(GetUserInfoRequest) returns (GetUserInfoResponse) {">`GetUserInfo`</SwmToken>, and <SwmToken path="pkg/apiclient/info/info.proto" pos="55:3:3" line-data="  rpc CollectEvent(CollectEventRequest) returns (CollectEventResponse) {">`CollectEvent`</SwmToken>.

## <SwmToken path="pkg/apiclient/info/info.proto" pos="45:2:2" line-data="service InfoService {">`InfoService`</SwmToken> Overview

The <SwmToken path="pkg/apiclient/info/info.proto" pos="45:2:2" line-data="service InfoService {">`InfoService`</SwmToken> includes methods such as <SwmToken path="pkg/apiclient/info/info.proto" pos="46:3:3" line-data="  rpc GetInfo(GetInfoRequest) returns (InfoResponse) {">`GetInfo`</SwmToken>, <SwmToken path="pkg/apiclient/info/info.pb.go" pos="512:9:9" line-data="func (c *infoServiceClient) GetVersion(ctx context.Context, in *GetVersionRequest, opts ...grpc.CallOption) (*v1alpha1.Version, error) {">`GetVersion`</SwmToken>, <SwmToken path="pkg/apiclient/info/info.proto" pos="52:3:3" line-data="  rpc GetUserInfo(GetUserInfoRequest) returns (GetUserInfoResponse) {">`GetUserInfo`</SwmToken>, and <SwmToken path="pkg/apiclient/info/info.proto" pos="55:3:3" line-data="  rpc CollectEvent(CollectEventRequest) returns (CollectEventResponse) {">`CollectEvent`</SwmToken>. These methods are used to retrieve system information, version details, user information, and to collect events, respectively.

## <SwmToken path="pkg/apiclient/info/info.proto" pos="46:3:3" line-data="  rpc GetInfo(GetInfoRequest) returns (InfoResponse) {">`GetInfo`</SwmToken> Method

The <SwmToken path="pkg/apiclient/info/info.proto" pos="46:3:3" line-data="  rpc GetInfo(GetInfoRequest) returns (InfoResponse) {">`GetInfo`</SwmToken> method returns an <SwmToken path="pkg/apiclient/info/info.proto" pos="46:11:11" line-data="  rpc GetInfo(GetInfoRequest) returns (InfoResponse) {">`InfoResponse`</SwmToken> containing details like the managed namespace, links, modals, navigation color, and columns.

<SwmSnippet path="/pkg/apiclient/info/info.proto" line="45">

---

The <SwmToken path="pkg/apiclient/info/info.proto" pos="46:3:3" line-data="  rpc GetInfo(GetInfoRequest) returns (InfoResponse) {">`GetInfo`</SwmToken> method is defined in the <SwmToken path="pkg/apiclient/info/info.proto" pos="45:2:2" line-data="service InfoService {">`InfoService`</SwmToken> and is accessed via a GET request to <SwmPath>[pkg/apiclient/info/](pkg/apiclient/info/)</SwmPath>.

```protocol buffer
service InfoService {
  rpc GetInfo(GetInfoRequest) returns (InfoResponse) {
    option (google.api.http).get = "/api/v1/info";
  }
```

---

</SwmSnippet>

## <SwmToken path="pkg/apiclient/info/info.proto" pos="46:11:11" line-data="  rpc GetInfo(GetInfoRequest) returns (InfoResponse) {">`InfoResponse`</SwmToken> Type

The <SwmToken path="pkg/apiclient/info/info.proto" pos="46:11:11" line-data="  rpc GetInfo(GetInfoRequest) returns (InfoResponse) {">`InfoResponse`</SwmToken> type includes fields like <SwmToken path="pkg/apiclient/info/info.pb.go" pos="71:17:17" line-data="	ManagedNamespace string           `protobuf:&quot;bytes,1,opt,name=managedNamespace,proto3&quot; json:&quot;managedNamespace,omitempty&quot;`">`managedNamespace`</SwmToken>, <SwmToken path="pkg/apiclient/info/info.pb.go" pos="72:22:22" line-data="	Links            []*v1alpha1.Link `protobuf:&quot;bytes,2,rep,name=links,proto3&quot; json:&quot;links,omitempty&quot;`">`links`</SwmToken>, <SwmToken path="pkg/apiclient/info/info.pb.go" pos="73:5:5" line-data="	// which modals to show">`modals`</SwmToken>, <SwmToken path="pkg/apiclient/info/info.pb.go" pos="75:17:17" line-data="	NavColor             string             `protobuf:&quot;bytes,4,opt,name=navColor,proto3&quot; json:&quot;navColor,omitempty&quot;`">`navColor`</SwmToken>, and <SwmToken path="pkg/apiclient/info/info.pb.go" pos="76:22:22" line-data="	Columns              []*v1alpha1.Column `protobuf:&quot;bytes,5,rep,name=columns,proto3&quot; json:&quot;columns,omitempty&quot;`">`columns`</SwmToken>, which are returned by the <SwmToken path="pkg/apiclient/info/info.proto" pos="46:3:3" line-data="  rpc GetInfo(GetInfoRequest) returns (InfoResponse) {">`GetInfo`</SwmToken> method.

<SwmSnippet path="/pkg/apiclient/info/info.pb.go" line="70">

---

The <SwmToken path="pkg/apiclient/info/info.pb.go" pos="70:2:2" line-data="type InfoResponse struct {">`InfoResponse`</SwmToken> struct definition includes fields for managed namespace, links, modals, navigation color, and columns.

```go
type InfoResponse struct {
	ManagedNamespace string           `protobuf:"bytes,1,opt,name=managedNamespace,proto3" json:"managedNamespace,omitempty"`
	Links            []*v1alpha1.Link `protobuf:"bytes,2,rep,name=links,proto3" json:"links,omitempty"`
	// which modals to show
	Modals               map[string]bool    `protobuf:"bytes,3,rep,name=modals,proto3" json:"modals,omitempty" protobuf_key:"bytes,1,opt,name=key,proto3" protobuf_val:"varint,2,opt,name=value,proto3"`
	NavColor             string             `protobuf:"bytes,4,opt,name=navColor,proto3" json:"navColor,omitempty"`
	Columns              []*v1alpha1.Column `protobuf:"bytes,5,rep,name=columns,proto3" json:"columns,omitempty"`
	XXX_NoUnkeyedLiteral struct{}           `json:"-"`
	XXX_unrecognized     []byte             `json:"-"`
	XXX_sizecache        int32              `json:"-"`
}
```

---

</SwmSnippet>

## <SwmToken path="pkg/apiclient/info/info.proto" pos="52:3:3" line-data="  rpc GetUserInfo(GetUserInfoRequest) returns (GetUserInfoResponse) {">`GetUserInfo`</SwmToken> Method

The <SwmToken path="pkg/apiclient/info/info.proto" pos="52:3:3" line-data="  rpc GetUserInfo(GetUserInfoRequest) returns (GetUserInfoResponse) {">`GetUserInfo`</SwmToken> method provides user-related information such as issuer, subject, groups, email, and service account details.

<SwmSnippet path="/pkg/apiclient/info/info.proto" line="52">

---

The <SwmToken path="pkg/apiclient/info/info.proto" pos="52:3:3" line-data="  rpc GetUserInfo(GetUserInfoRequest) returns (GetUserInfoResponse) {">`GetUserInfo`</SwmToken> method is part of the <SwmToken path="pkg/apiclient/info/info.proto" pos="45:2:2" line-data="service InfoService {">`InfoService`</SwmToken> and is accessed via a GET request to <SwmPath>[ui/src/app/userinfo/](ui/src/app/userinfo/)</SwmPath>.

```protocol buffer
  rpc GetUserInfo(GetUserInfoRequest) returns (GetUserInfoResponse) {
    option (google.api.http).get = "/api/v1/userinfo";
  }
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apiclient/info/info.pb.go" line="512">

---

The <SwmToken path="pkg/apiclient/info/info.proto" pos="52:3:3" line-data="  rpc GetUserInfo(GetUserInfoRequest) returns (GetUserInfoResponse) {">`GetUserInfo`</SwmToken> function implementation retrieves user-related information.

```go
func (c *infoServiceClient) GetVersion(ctx context.Context, in *GetVersionRequest, opts ...grpc.CallOption) (*v1alpha1.Version, error) {
	out := new(v1alpha1.Version)
```

---

</SwmSnippet>

<SwmSnippet path="/pkg/apiclient/info/info.pb.go" line="512">

---

The <SwmToken path="pkg/apiclient/info/info.pb.go" pos="512:9:9" line-data="func (c *infoServiceClient) GetVersion(ctx context.Context, in *GetVersionRequest, opts ...grpc.CallOption) (*v1alpha1.Version, error) {">`GetVersion`</SwmToken> function implementation retrieves version details of the system.

```go
func (c *infoServiceClient) GetVersion(ctx context.Context, in *GetVersionRequest, opts ...grpc.CallOption) (*v1alpha1.Version, error) {
	out := new(v1alpha1.Version)
```

---

</SwmSnippet>

## <SwmToken path="pkg/apiclient/info/info.proto" pos="55:3:3" line-data="  rpc CollectEvent(CollectEventRequest) returns (CollectEventResponse) {">`CollectEvent`</SwmToken> Method

The <SwmToken path="pkg/apiclient/info/info.proto" pos="55:3:3" line-data="  rpc CollectEvent(CollectEventRequest) returns (CollectEventResponse) {">`CollectEvent`</SwmToken> method is used to collect and log events within the system.

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
