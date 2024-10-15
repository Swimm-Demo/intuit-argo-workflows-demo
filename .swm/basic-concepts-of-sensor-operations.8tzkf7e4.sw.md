---
title: Basic Concepts of Sensor Operations
---
## Overview

Sensor is a core component in the Apiclient package, responsible for handling various sensor-related operations. It includes functionalities for listing, creating, updating, deleting, and retrieving sensors within a specified namespace. The `SensorServiceClient` interface defines the methods available for interacting with sensors, such as <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="75:3:3" line-data="  rpc ListSensors(ListSensorsRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.SensorList) {">`ListSensors`</SwmToken>, <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="84:3:3" line-data="  rpc CreateSensor(CreateSensorRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.Sensor) {">`CreateSensor`</SwmToken>, <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="90:3:3" line-data="  rpc UpdateSensor(UpdateSensorRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.Sensor) {">`UpdateSensor`</SwmToken>, <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="96:3:3" line-data="  rpc DeleteSensor(DeleteSensorRequest) returns (DeleteSensorResponse) {">`DeleteSensor`</SwmToken>, and <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="99:3:3" line-data="  rpc GetSensor(GetSensorRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.Sensor) {">`GetSensor`</SwmToken>.

## gRPC and HTTP Communication

Each method in the `SensorServiceClient` interface corresponds to a specific gRPC call, facilitating communication between the client and the server. The <SwmPath>[pkg/apiclient/sensor/sensor.proto](pkg/apiclient/sensor/sensor.proto)</SwmPath> file defines the structure of the requests and responses for these operations, ensuring consistent data exchange. Additionally, the <SwmPath>[pkg/apiclient/sensor/sensor.pb.gw.go](pkg/apiclient/sensor/sensor.pb.gw.go)</SwmPath> file contains the implementation for handling HTTP requests and forwarding them to the appropriate gRPC methods.

## Updating a Sensor

To update an existing sensor, you can use the `sensorServiceUpdateSensor` method. This method sends a PUT request to the specified namespace and sensor name to update the sensor's details.

## Retrieving a Sensor

To retrieve a sensor's details, you can use the `sensorServiceGetSensor` method. This method sends a GET request to the specified namespace and sensor name to fetch the sensor's information.

## Main Functions

There are several main functions in this folder. Some of them are `sensorServiceCreateSensor`, `sensorServiceDeleteSensor`, `sensorServiceGetSensor`, `sensorServiceListSensors`, `sensorServiceSensorsLogs`, `sensorServiceUpdateSensor`, and `sensorServiceWatchSensors`. We will dive a little into `sensorServiceCreateSensor` and `sensorServiceDeleteSensor`.

### sensorServiceCreateSensor

The `sensorServiceCreateSensor` function is used to create a new sensor within a specified namespace. It sends a POST request to the server with the sensor details and returns the created sensor object.

### sensorServiceDeleteSensor

The `sensorServiceDeleteSensor` function is used to delete an existing sensor by its name within a specified namespace. It sends a DELETE request to the server and returns a response indicating the success or failure of the operation.

## Sensor APIs

The Sensor APIs provide endpoints for various sensor operations.

### <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="75:3:3" line-data="  rpc ListSensors(ListSensorsRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.SensorList) {">`ListSensors`</SwmToken>

The <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="75:3:3" line-data="  rpc ListSensors(ListSensorsRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.SensorList) {">`ListSensors`</SwmToken> endpoint is used to retrieve a list of sensors within a specified namespace. It takes a <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="75:5:5" line-data="  rpc ListSensors(ListSensorsRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.SensorList) {">`ListSensorsRequest`</SwmToken> message containing the namespace and list options, and returns a <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="75:27:27" line-data="  rpc ListSensors(ListSensorsRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.SensorList) {">`SensorList`</SwmToken> message. The HTTP GET method is used for this endpoint, with the URL pattern <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="76:16:25" line-data="    option (google.api.http).get = &quot;/api/v1/sensors/{namespace}&quot;;">`/api/v1/sensors/{namespace}`</SwmToken>.

<SwmSnippet path="/pkg/apiclient/sensor/sensor.proto" line="74">

---

The <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="75:3:3" line-data="  rpc ListSensors(ListSensorsRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.SensorList) {">`ListSensors`</SwmToken> method in the <SwmPath>[pkg/apiclient/sensor/sensor.proto](pkg/apiclient/sensor/sensor.proto)</SwmPath> file defines the gRPC call and HTTP GET method for listing sensors.

```protocol buffer
service SensorService {
  rpc ListSensors(ListSensorsRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.SensorList) {
    option (google.api.http).get = "/api/v1/sensors/{namespace}";
  }
```

---

</SwmSnippet>

### <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="84:3:3" line-data="  rpc CreateSensor(CreateSensorRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.Sensor) {">`CreateSensor`</SwmToken>

The <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="84:3:3" line-data="  rpc CreateSensor(CreateSensorRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.Sensor) {">`CreateSensor`</SwmToken> endpoint is used to create a new sensor within a specified namespace. It takes a <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="84:5:5" line-data="  rpc CreateSensor(CreateSensorRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.Sensor) {">`CreateSensorRequest`</SwmToken> message containing the namespace, sensor details, and create options, and returns a <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="84:27:27" line-data="  rpc CreateSensor(CreateSensorRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.Sensor) {">`Sensor`</SwmToken> message. The HTTP POST method is used for this endpoint, with the URL pattern <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="76:16:25" line-data="    option (google.api.http).get = &quot;/api/v1/sensors/{namespace}&quot;;">`/api/v1/sensors/{namespace}`</SwmToken> and the request body containing the sensor details.

<SwmSnippet path="/pkg/apiclient/sensor/sensor.proto" line="84">

---

The <SwmToken path="pkg/apiclient/sensor/sensor.proto" pos="84:3:3" line-data="  rpc CreateSensor(CreateSensorRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.Sensor) {">`CreateSensor`</SwmToken> method in the <SwmPath>[pkg/apiclient/sensor/sensor.proto](pkg/apiclient/sensor/sensor.proto)</SwmPath> file defines the gRPC call and HTTP POST method for creating a sensor.

```protocol buffer
  rpc CreateSensor(CreateSensorRequest) returns (github.com.argoproj.argo_events.pkg.apis.sensor.v1alpha1.Sensor) {
    option (google.api.http) = {
      post : "/api/v1/sensors/{namespace}"
      body : "*"
    };
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
