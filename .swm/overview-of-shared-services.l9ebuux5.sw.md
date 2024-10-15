---
title: Overview of Shared Services
---
# What are Shared Services

Shared Services are a collection of utilities that provide various functionalities to interact with different aspects of the application. These services include handling workflows, cron workflows, events, event sources, sensors, and workflow templates. Each service is responsible for making API requests to perform actions such as creating, listing, updating, and deleting resources.

## Example Services

For example, the <SwmToken path="ui/src/app/shared/services/index.ts" pos="23:4:4" line-data="    workflows: WorkflowsService,">`WorkflowsService`</SwmToken> handles operations related to workflows, including creating new workflows, listing existing ones, and managing workflow states. Similarly, the <SwmToken path="ui/src/app/shared/services/index.ts" pos="22:4:4" line-data="    info: InfoService,">`InfoService`</SwmToken> provides methods to fetch information about the application, such as version details and user information.

<SwmSnippet path="/ui/src/app/shared/services/index.ts" line="21">

---

The <SwmToken path="ui/src/app/shared/services/index.ts" pos="21:4:4" line-data="export const services: Services = {">`services`</SwmToken> constant aggregates all individual services like <SwmToken path="ui/src/app/shared/services/index.ts" pos="22:4:4" line-data="    info: InfoService,">`InfoService`</SwmToken>, <SwmToken path="ui/src/app/shared/services/index.ts" pos="23:4:4" line-data="    workflows: WorkflowsService,">`WorkflowsService`</SwmToken>, and others, making them accessible from a single object.

```typescript
export const services: Services = {
    info: InfoService,
    workflows: WorkflowsService,
    workflowTemplate: WorkflowTemplateService,
    clusterWorkflowTemplate: ClusterWorkflowTemplateService,
    event: EventService,
    eventSource: EventSourceService,
    sensor: SensorService,
    cronWorkflows: CronWorkflowService
};
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/shared/services/workflows-service.ts" line="26">

---

The <SwmToken path="ui/src/app/shared/services/workflows-service.ts" pos="26:4:4" line-data="export const WorkflowsService = {">`WorkflowsService`</SwmToken> provides methods to create, list, and manage workflows by making API requests.

```typescript
export const WorkflowsService = {
    create(workflow: Workflow, namespace: string) {
        return requests
            .post(`api/v1/workflows/${namespace}`)
            .send({workflow})
            .then(res => res.body as Workflow);
    },
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/shared/services/info-service.ts" line="7">

---

The <SwmToken path="ui/src/app/shared/services/info-service.ts" pos="7:4:4" line-data="export const InfoService = {">`InfoService`</SwmToken> offers methods to get application information, version details, and user information by making API requests.

```typescript
export const InfoService = {
    getInfo() {
        if (info) {
            return info;
        }
        info = requests.get(`api/v1/info`).then(res => res.body as Info);
        return info;
    },

    getVersion() {
        return requests.get(`api/v1/version`).then(res => res.body as Version);
    },

    getUserInfo() {
        return requests.get(`api/v1/userinfo`).then(res => res.body as GetUserInfoResponse);
    },

    collectEvent(name: string) {
        return requests.post(`api/v1/tracking/event`).send({name});
    }
```

---

</SwmSnippet>

## Usage of Services

The <SwmToken path="ui/src/app/shared/services/index.ts" pos="21:4:4" line-data="export const services: Services = {">`services`</SwmToken> constant is used extensively throughout the application to perform various operations. Below are some examples of how these services are utilized.

<SwmSnippet path="/ui/src/app/shared/workflow-operations-map.tsx" line="32">

---

The <SwmToken path="ui/src/app/shared/workflow-operations-map.tsx" pos="32:13:13" line-data="        action: (wf: Workflow) =&gt; services.workflows.retry(wf.metadata.name, wf.metadata.namespace, null)">`services`</SwmToken> constant is used to perform workflow operations like retrying, resubmitting, and suspending workflows.

```tsx
        action: (wf: Workflow) => services.workflows.retry(wf.metadata.name, wf.metadata.namespace, null)
    },
    RESUBMIT: {
        title: 'RESUBMIT',
        iconClassName: 'fa fa-plus-circle',
        disabled: () => false,
        action: (wf: Workflow) => services.workflows.resubmit(wf.metadata.name, wf.metadata.namespace, null)
    },
    SUSPEND: {
        title: 'SUSPEND',
        iconClassName: 'fa fa-pause',
        disabled: (wf: Workflow) => !isWorkflowRunning(wf) || isWorkflowSuspended(wf),
        action: (wf: Workflow) => services.workflows.suspend(wf.metadata.name, wf.metadata.namespace)
    },
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/event-flow/event-flow-page.tsx" line="88">

---

The <SwmToken path="ui/src/app/event-flow/event-flow-page.tsx" pos="89:6:6" line-data="            () =&gt; services.eventSource.list(namespace),">`services`</SwmToken> constant is used to list and watch event sources and sensors.

```tsx
        const listWatch = new ListWatch<EventSource>(
            () => services.eventSource.list(namespace),
            () => services.eventSource.watch(namespace),
            () => setError(null),
            () => setError(null),
            items => setEventSources([...items]),
            setError
        );
        listWatch.start();
        return () => listWatch.stop();
    }, [namespace]);
    useEffect(() => {
        const listWatch = new ListWatch<Sensor>(
            () => services.sensor.list(namespace),
            () => services.sensor.watch(namespace),
            () => setError(null),
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/workflow-templates/workflow-template-details.tsx" line="62">

---

The <SwmToken path="ui/src/app/workflow-templates/workflow-template-details.tsx" pos="63:1:1" line-data="        services.workflowTemplate">`services`</SwmToken> constant is used to get workflow templates and list workflows associated with a specific template.

```tsx
    useEffect(() => {
        services.workflowTemplate
            .get(name, namespace)
            .then(resetTemplate)
            .then(() => setError(null))
            .catch(setError);
    }, [name, namespace]);

    useEffect(() => {
        (async () => {
            const workflowList = await services.workflows.list(namespace, null, [`${models.labels.workflowTemplate}=${name}`], {limit: 50});
            const workflowsInfo = await services.info.getInfo();

            setWorkflows(workflowList.items);
            setColumns(workflowsInfo.columns);
        })();
    }, []);
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/cron-workflows/cron-workflow-details.tsx" line="63">

---

The <SwmToken path="ui/src/app/cron-workflows/cron-workflow-details.tsx" pos="64:1:1" line-data="        services.cronWorkflows">`services`</SwmToken> constant is used to get cron workflows and list workflows associated with a specific cron workflow.

```tsx
    useEffect(() => {
        services.cronWorkflows
            .get(name, namespace)
            .then(resetCronWorkflow)
            .then(() => setError(null))
            .catch(setError);
    }, [namespace, name]);

    useEffect(() => {
        (async () => {
            const workflowList = await services.workflows.list(namespace, null, [`${models.labels.cronWorkflow}=${name}`], {limit: 50});
            const workflowsInfo = await services.info.getInfo();

            setWorkflows(workflowList.items);
            setColumns(workflowsInfo.columns);
        })();
    }, []);
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/cluster-workflow-templates/cluster-workflow-template-details.tsx" line="56">

---

The <SwmToken path="ui/src/app/cluster-workflow-templates/cluster-workflow-template-details.tsx" pos="57:9:9" line-data="                const newTemplate = await services.clusterWorkflowTemplate.get(name);">`services`</SwmToken> constant is used to get cluster workflow templates and list workflows associated with a specific cluster workflow template.

```tsx
            try {
                const newTemplate = await services.clusterWorkflowTemplate.get(name);
                resetTemplate(newTemplate);
                setError(null);
            } catch (err) {
                setError(err);
            }
        })();
    }, [name]);

    useEffect(() => {
        (async () => {
            try {
                const workflowList = await services.workflows.list('', null, [`${models.labels.clusterWorkflowTemplate}=${name}`], {limit: 50});
                const info = await services.info.getInfo();

                setWorkflows(workflowList.items);
                setColumns(info.columns);
                setNamespace(nsUtils.getNamespaceWithDefault(info.managedNamespace));
                setError(null);
            } catch (err) {
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/workflows/components/workflow-details/workflow-details.tsx" line="169">

---

The <SwmToken path="ui/src/app/workflows/components/workflow-details/workflow-details.tsx" pos="170:9:9" line-data="                const info = await services.info.getInfo();">`services`</SwmToken> constant is used to get workflow details, delete workflows, and watch workflow updates.

```tsx
            try {
                const info = await services.info.getInfo();
                setLinks(info.links);
            } catch (err) {
                setError(err);
            }
        })();
    }, []);

    useCollectEvent('openedWorkflowDetails');

    useEffect(() => {
        setParameters(getInputParametersForNode(nodeId));
    }, [nodeId, workflow]);

    const parsedSidePanel = parseSidePanelParam(sidePanel);

    function getItems() {
        const workflowOperationsMap: WorkflowOperations = Operations.WorkflowOperationsMap;
        const items = Object.keys(workflowOperationsMap)
            .filter(actionName => !workflowOperationsMap[actionName].disabled(workflow))
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/app-router.tsx" line="67">

---

The <SwmToken path="ui/src/app/app-router.tsx" pos="68:1:1" line-data="        services.info.getUserInfo().then(userInfo =&gt; {">`services`</SwmToken> constant is used to get user information and application version details during the app initialization.

```tsx
    useEffect(() => {
        services.info.getUserInfo().then(userInfo => {
            nsUtils.setUserNamespace(userInfo.serviceAccountNamespace);
            setNamespace(nsUtils.getCurrentNamespace());
        });
        services.info
            .getInfo()
            .then(info => {
                nsUtils.setManagedNamespace(info.managedNamespace);
                setNamespace(nsUtils.getCurrentNamespace());
                setModals(info.modals);
                setNavBarBackgroundColor(info.navColor);
            })
            .then(() => services.info.getVersion())
            .then(setVersion)
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/sensors/sensor-details.tsx" line="58">

---

The <SwmToken path="ui/src/app/sensors/sensor-details.tsx" pos="59:1:1" line-data="        services.sensor">`services`</SwmToken> constant is used to get, update, and delete sensor details.

```tsx
    useEffect(() => {
        services.sensor
            .get(name, namespace)
            .then(resetSensor)
            .then(() => setError(null))
            .catch(setError);
    }, [namespace, name]);

    useCollectEvent('openedSensorDetails');

    const selected = (() => {
        if (!selectedLogNode) {
            return;
        }
        const x = ID.split(selectedLogNode);
        return {...x};
    })();

    return (
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/event-sources/event-source-details.tsx" line="70">

---

The <SwmToken path="ui/src/app/event-sources/event-source-details.tsx" pos="71:9:9" line-data="                const newEventSource = await services.eventSource.get(name, namespace);">`services`</SwmToken> constant is used to get, update, and delete event source details.

```tsx
            try {
                const newEventSource = await services.eventSource.get(name, namespace);
                resetEventSource(newEventSource);
                setError(null);
            } catch (err) {
                setError(err);
            }
        })();
    }, [name, namespace]);

    useCollectEvent('openedEventSourceDetails');

    return (
        <Page
            title='Event Source Details'
            toolbar={{
                breadcrumbs: [
                    {title: 'Event Source', path: uiUrl('event-sources')},
                    {title: namespace, path: uiUrl('event-sources/' + namespace)},
                    {title: name, path: uiUrl('event-sources/' + namespace + '/' + name)}
                ],
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/workflows/components/workflows-list/workflows-list.tsx" line="111">

---

The <SwmToken path="ui/src/app/workflows/components/workflows-list/workflows-list.tsx" pos="112:9:9" line-data="            const info = await services.info.getInfo();">`services`</SwmToken> constant is used to list workflows and watch workflow updates.

```tsx
        (async () => {
            const info = await services.info.getInfo();
            setLinks((info.links || []).filter(link => link.scope === 'workflow-list'));
            setColumns(info.columns);
        })();
    }, []);

    // save history and localStorage
    useEffect(() => {
        // add empty selectedPhases + selectedLabels for forward-compat w/ old version: previous code relies on them existing, so if you move up a version and back down, it breaks
        const options = {selectedPhases: [], selectedLabels: []} as unknown as WorkflowListRenderOptions;
        options.phases = phases;
        options.labels = labels;
        if (pagination.limit) {
            options.paginationLimit = pagination.limit;
        }
        storage.setItem('options', options, {} as WorkflowListRenderOptions);

        const params = new URLSearchParams();
        phases?.forEach(phase => params.append('phase', phase));
        labels?.forEach(label => params.append('label', label));
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/workflows/components/workflow-details/artifact-panel.tsx" line="27">

---

The <SwmToken path="ui/src/app/workflows/components/workflow-details/artifact-panel.tsx" pos="28:7:7" line-data="    const downloadUrl = services.workflows.getArtifactDownloadUrl(workflow, artifact.nodeId, artifact.name, archived, input);">`services`</SwmToken> constant is used to get artifact download URLs and paths for workflows.

```tsx
    const input = artifact.artifactNameDiscriminator === 'input';
    const downloadUrl = services.workflows.getArtifactDownloadUrl(workflow, artifact.nodeId, artifact.name, archived, input);

    const urn = artifactURN(artifact, artifactRepository);
    const key = artifactKey(artifact);
    const isDir = key.endsWith('/');
    const filename = key.split('/').pop();
    const ext = filename.split('.').pop();

    const [show, setShow] = useState(false);
    const [error, setError] = useState<Error>();
    const [object, setObject] = useState<any>();

    const tgz = !input && !artifact.archive?.none; // the key can be wrong about the file type
    const supported = !tgz && (isDir || ['gif', 'jpg', 'jpeg', 'json', 'html', 'png', 'txt'].includes(ext));
    useEffect(() => setShow(supported), [downloadUrl, ext]);

    useEffect(() => {
        setObject(null);
        setError(null);
        if (ext === 'json') {
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/reports/reports-filters.tsx" line="65">

---

The <SwmToken path="ui/src/app/reports/reports-filters.tsx" pos="66:9:9" line-data="                            const list = await services.workflowTemplate.list(namespace, []);">`services`</SwmToken> constant is used to list workflow templates and cron workflows for report filters.

```tsx
                        load={async () => {
                            const list = await services.workflowTemplate.list(namespace, []);
                            return (list.items || []).map(x => x.metadata.name);
                        }}
                        onChange={value => setWorkflowTemplate(value)}
                    />
                </div>
                <div className=' columns small-12 xlarge-12'>
                    <p className='wf-filters-container__title'>Cron Workflow</p>
                    <DataLoaderDropdown
                        load={async () => {
                            const list = await services.cronWorkflows.list(namespace);
                            return list.map(x => x.metadata.name);
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/workflows/components/resubmit-workflow-panel.tsx" line="35">

---

The <SwmToken path="ui/src/app/workflows/components/resubmit-workflow-panel.tsx" pos="36:5:5" line-data="                ? await services.workflows.resubmitArchived(props.workflow.metadata.uid, props.workflow.metadata.namespace, opts)">`services`</SwmToken> constant is used to resubmit archived and non-archived workflows.

```tsx
            const submitted = props.isArchived
                ? await services.workflows.resubmitArchived(props.workflow.metadata.uid, props.workflow.metadata.namespace, opts)
                : await services.workflows.resubmit(props.workflow.metadata.name, props.workflow.metadata.namespace, opts);
            navigation.goto(uiUrl(`workflows/${submitted.metadata.namespace}/${submitted.metadata.name}`));
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/workflows/components/workflow-creator.tsx" line="25">

---

The <SwmToken path="ui/src/app/workflows/components/workflow-creator.tsx" pos="26:1:1" line-data="        services.workflowTemplate">`services`</SwmToken> constant is used to list workflow templates and create new workflows.

```tsx
    useEffect(() => {
        services.workflowTemplate
            .list(namespace, [])
            .then(list => list.items || [])
            .then(setWorkflowTemplates)
            .catch(setError);
    }, [namespace]);

    useEffect(() => {
        if (stage !== 'full-editor') return;
        if (!workflowTemplate) {
            setWorkflow(exampleWorkflow(nsUtils.getNamespaceWithDefault(namespace)));
            return;
        }

        setWorkflow({
            metadata: {
                generateName: workflowTemplate.metadata.name + '-',
                namespace,
                labels: {
                    'workflows.argoproj.io/workflow-template': workflowTemplate.metadata.name,
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/workflows/components/retry-workflow-panel.tsx" line="39">

---

The <SwmToken path="ui/src/app/workflows/components/retry-workflow-panel.tsx" pos="40:5:5" line-data="                    ? await services.workflows.retryArchived(props.workflow.metadata.uid, props.workflow.metadata.namespace, opts)">`services`</SwmToken> constant is used to retry archived and non-archived workflows.

```tsx
                props.isArchived && !props.isWorkflowInCluster
                    ? await services.workflows.retryArchived(props.workflow.metadata.uid, props.workflow.metadata.namespace, opts)
                    : await services.workflows.retry(props.workflow.metadata.name, props.workflow.metadata.namespace, opts);
            navigation.goto(uiUrl(`workflows/${submitted.metadata.namespace}/${submitted.metadata.name}#`)); // add # at the end to reset query params to close panel
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/workflows/components/workflow-logs-viewer/workflow-logs-viewer.tsx" line="107">

---

The <SwmToken path="ui/src/app/workflows/components/workflow-logs-viewer/workflow-logs-viewer.tsx" pos="107:7:7" line-data="        const source = services.workflows.getContainerLogs(workflow, podName, nodeId, selectedContainer, grep, archived).pipe(">`services`</SwmToken> constant is used to get container logs and artifact logs for workflows.

```tsx
        const source = services.workflows.getContainerLogs(workflow, podName, nodeId, selectedContainer, grep, archived).pipe(
            // extract message from LogEntry
            map(e => {
                const values: string[] = [];
                const content = e.content;
                if (selectedJsonFields.values.length > 0) {
                    try {
                        const json = JSON.parse(content);
                        selectedJsonFields.values.forEach(selectedJsonField => {
                            const value = extractJsonValue(json, selectedJsonField);
                            if (value) {
                                values.push(value);
                            }
                        });
                    } catch (e) {
                        // if not json, show content directly
                    }
                }
                if (values.length === 0) {
                    values.push(content);
                }
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/workflows/components/workflows-toolbar/workflows-toolbar.tsx" line="75">

---

The <SwmToken path="ui/src/app/workflows/components/workflows-toolbar/workflows-toolbar.tsx" pos="76:1:1" line-data="                        services.workflows.delete(wf.metadata.name, wf.metadata.namespace).catch(reason =&gt;">`services`</SwmToken> constant is used to delete workflows and archived workflows.

```tsx
                    promises.push(
                        services.workflows.delete(wf.metadata.name, wf.metadata.namespace).catch(reason =>
                            notifications.show({
                                content: `Unable to delete workflow ${wf.metadata.name} in the cluster: ${reason.toString()}`,
                                type: NotificationType.Error
                            })
                        )
                    );
                }
                if (deleteArchived && isArchivedWorkflow(wf)) {
                    promises.push(
                        services.workflows.deleteArchived(wf.metadata.uid, wf.metadata.namespace).catch(reason =>
                            notifications.show({
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
