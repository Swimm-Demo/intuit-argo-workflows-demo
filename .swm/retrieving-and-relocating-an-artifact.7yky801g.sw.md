---
title: Retrieving and Relocating an Artifact
---
This document will cover the process of retrieving and relocating an artifact, which includes:

1. Retrieving the artifact and its associated driver
2. Determining the artifact's location
3. Relocating the artifact if necessary.

Technical document: <SwmLink doc-title="Retrieving and Relocating an Artifact">[Retrieving and Relocating an Artifact](/.swm/retrieving-and-relocating-an-artifact.nv7up0rb.sw.md)</SwmLink>

# [Retrieving the Artifact and Driver](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v/docs/nv7up0rb#retrieving-and-relocating-the-artifact)

The process begins with retrieving the artifact and its associated driver. This involves checking the node status to determine if the artifact is an input or output. Based on this, the artifact is retrieved from the node's inputs or outputs. If the artifact is not found, an error is returned. This step ensures that we have the correct artifact and driver to proceed with further actions.

# [Determining the Artifact's Location](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v/docs/nv7up0rb#relocating-the-artifact)

Once the artifact is retrieved, the next step is to determine its location. The location can be defined in various places such as the artifact itself, controller configmap, workflow spec, or template. If the artifact does not already have a location, the location information is copied from the provided parameter. If the provided location is nil, an error is returned. This step ensures that the artifact's location is correctly identified and set.

# [Relocating the Artifact if Necessary](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v/docs/nv7up0rb#getting-the-artifact-key)

If the artifact needs to be relocated, the process involves copying all location information from the provided parameter to the artifact, except for the key. The key is then retrieved for the artifact location. This step ensures that the artifact is relocated to the correct location and the key is updated accordingly.

# [Append Filename to Artifact Key](http://localhost:5001/repos/Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v/docs/nv7up0rb#getting-the-artifact-location-type)

Finally, if a filename is provided, it is appended to the artifact key. This ensures that the artifact is correctly identified and can be accessed using the updated key. This step is crucial for maintaining the integrity and accessibility of the artifact.

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
