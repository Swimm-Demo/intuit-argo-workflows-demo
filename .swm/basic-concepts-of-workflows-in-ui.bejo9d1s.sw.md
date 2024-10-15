---
title: Basic Concepts of Workflows in UI
---
# Basic Concepts of Workflows in UI

Workflows are a core component that allows users to define and manage multi-step processes. Each workflow consists of a series of tasks, where each task is executed in a container. Workflows can be visualized and managed through the user interface, providing a clear view of the execution status and results.

## Workflow Actions

The user interface supports various actions on workflows, such as retrying, resubmitting, suspending, resuming, stopping, terminating, and deleting. Users can filter workflows based on different criteria like phases, labels, and time filters.

## Workflow Details

The interface provides detailed information about each workflow, including its status, progress, duration, and associated resources. The <SwmToken path="ui/src/app/workflows/components/workflow-details/workflow-details.tsx" pos="93:4:4" line-data="export function WorkflowDetails({history, location, match}: RouteComponentProps&lt;any&gt;) {">`WorkflowDetails`</SwmToken> component is responsible for displaying this information and allows users to perform actions on the workflow.

<SwmSnippet path="/ui/src/app/workflows/components/workflow-details/workflow-details.tsx" line="93">

---

The <SwmToken path="ui/src/app/workflows/components/workflow-details/workflow-details.tsx" pos="93:4:4" line-data="export function WorkflowDetails({history, location, match}: RouteComponentProps&lt;any&gt;) {">`WorkflowDetails`</SwmToken> component provides detailed information about a specific workflow, including its status, progress, duration, and associated resources. It also allows users to perform actions on the workflow.

```tsx
export function WorkflowDetails({history, location, match}: RouteComponentProps<any>) {
    // boiler-plate
    const {navigation, popup} = useContext(Context);
    const queryParams = new URLSearchParams(location.search);
    const namespace = match.params.namespace;
    const name = match.params.name;

    const [tab, setTab] = useState(queryParams.get('tab') || 'workflow');
    const [uid, setUid] = useState(queryParams.get('uid') || '');
    const [nodeId, setNodeId] = useState(queryParams.get('nodeId'));
    const [nodePanelView, setNodePanelView] = useState(queryParams.get('nodePanelView'));
    const [sidePanel, setSidePanel] = useState(queryParams.get('sidePanel'));
    const [parameters, setParameters] = useState<Parameter[]>([]);
    const sidePanelRef = useRef<HTMLDivElement>(null);
    const [workflow, setWorkflow] = useState<Workflow>();
    const [links, setLinks] = useState<Link[]>();
    const [error, setError] = useState<Error>();
    const selectedNode = workflow?.status?.nodes?.[nodeId];
    const selectedArtifact = workflow?.status && findArtifact(workflow.status, nodeId);
    const [selectedTemplateArtifactRepo, setSelectedTemplateArtifactRepo] = useState<ArtifactRepository>();
    const isSidePanelExpanded = !!(selectedNode || selectedArtifact);
```

---

</SwmSnippet>

## Workflow of Workflows

The Workflow of Workflows pattern involves a parent workflow triggering one or more child workflows, managing them, and acting on their results.

## Examples

You can use <SwmToken path="ui/src/app/workflows/components/workflow-details/workflow-details.tsx" pos="275:8:8" line-data="        if (workflow?.spec?.workflowTemplateRef) {">`workflowTemplateRef`</SwmToken> to trigger a workflow inline. First, define your workflow as a `workflowtemplate`.

## Workflow List

The <SwmToken path="ui/src/app/workflows/components/workflows-list/workflows-list.tsx" pos="54:4:4" line-data="export function WorkflowsList({match, location, history}: RouteComponentProps&lt;any&gt;) {">`WorkflowsList`</SwmToken> component in the user interface allows users to view and manage a list of workflows. It provides various actions such as retrying, resubmitting, suspending, resuming, stopping, terminating, and deleting workflows.

<SwmSnippet path="/ui/src/app/workflows/components/workflows-list/workflows-list.tsx" line="54">

---

The <SwmToken path="ui/src/app/workflows/components/workflows-list/workflows-list.tsx" pos="54:4:4" line-data="export function WorkflowsList({match, location, history}: RouteComponentProps&lt;any&gt;) {">`WorkflowsList`</SwmToken> component allows users to view and manage a list of workflows. It provides various actions such as retrying, resubmitting, suspending, resuming, stopping, terminating, and deleting workflows.

```tsx
export function WorkflowsList({match, location, history}: RouteComponentProps<any>) {
    const queryParams = new URLSearchParams(location.search);
    const {navigation} = useContext(Context);

    const [namespace, setNamespace] = useState(nsUtils.getNamespace(match.params.namespace) || '');
    const [pagination, setPagination] = useState<Pagination>(() => {
        const savedPaginationLimit = storage.getItem('options', {}).paginationLimit || undefined;
        return {
            offset: queryParams.get('offset') || undefined,
            limit: parseLimit(queryParams.get('limit')) || savedPaginationLimit || 50
        };
    });
    const [phases, setPhases] = useState<WorkflowPhase[]>(() => {
        const savedOptions = storage.getItem('options', {});
        // selectedPhases is a legacy name, used here for backward-compat with old storage
        const savedPhases = savedOptions.phases || savedOptions.selectedPhases || [];
        const phaseQueryParam = queryParams.getAll('phase') as WorkflowPhase[];
        return phaseQueryParam.length > 0 ? phaseQueryParam : savedPhases;
    });
    const [labels, setLabels] = useState<string[]>(() => {
        const savedOptions = storage.getItem('options', {});
```

---

</SwmSnippet>

## Workflow Summary Panel

The <SwmToken path="ui/src/app/workflows/components/workflow-summary-panel.tsx" pos="18:4:4" line-data="export const WorkflowSummaryPanel = (props: {workflow: Workflow}) =&gt; (">`WorkflowSummaryPanel`</SwmToken> component provides a summary of the workflow, displaying various attributes such as status, message, name, namespace, labels, start and finish times, duration, progress, creator, resources duration, and conditions. This component is essential for visualizing the workflow's current state and details.

<SwmSnippet path="/ui/src/app/workflows/components/workflow-summary-panel.tsx" line="18">

---

The <SwmToken path="ui/src/app/workflows/components/workflow-summary-panel.tsx" pos="18:4:4" line-data="export const WorkflowSummaryPanel = (props: {workflow: Workflow}) =&gt; (">`WorkflowSummaryPanel`</SwmToken> component provides a summary of the workflow, displaying various attributes such as status, message, name, namespace, labels, start and finish times, duration, progress, creator, resources duration, and conditions.

```tsx
export const WorkflowSummaryPanel = (props: {workflow: Workflow}) => (
    <Ticker disabled={props.workflow && props.workflow.status.phase !== NODE_PHASE.RUNNING}>
        {() => {
            const attributes: {title: string; value: any}[] = [
                {title: 'Status', value: <Phase value={props.workflow.status.phase} />},
                {title: 'Message', value: props.workflow.status.message},
                {title: 'Name', value: props.workflow.metadata.name},
                {title: 'Namespace', value: props.workflow.metadata.namespace},
                {title: 'From', value: <WorkflowFrom namespace={props.workflow.metadata.namespace} labels={props.workflow.metadata.labels} />},
                {
                    title: 'Labels',
                    value: (
                        <Consumer>
                            {ctx => (
                                <WorkflowLabels
                                    workflow={props.workflow}
                                    onChange={(key, value) => ctx.navigation.goto(uiUrl(`workflows/${props.workflow.metadata.namespace}?label=${key}=${value}`))}
                                />
                            )}
                        </Consumer>
                    )
```

---

</SwmSnippet>

## Workflow Node Info

The <SwmToken path="ui/src/app/workflows/components/workflow-details/workflow-details.tsx" pos="35:3:3" line-data="import {WorkflowNodeInfo} from &#39;../workflow-node-info/workflow-node-info&#39;;">`WorkflowNodeInfo`</SwmToken> component displays detailed information about a specific node within a workflow. It includes attributes like name, ID, type, start and end times, progress, and resources duration. This component is crucial for understanding the execution details of individual nodes within a workflow.

<SwmSnippet path="/ui/src/app/workflows/components/workflow-node-info/workflow-node-info.tsx" line="26">

---

The <SwmToken path="ui/src/app/workflows/components/workflow-details/workflow-details.tsx" pos="35:3:3" line-data="import {WorkflowNodeInfo} from &#39;../workflow-node-info/workflow-node-info&#39;;">`WorkflowNodeInfo`</SwmToken> component displays detailed information about a specific node within a workflow. It includes attributes like name, ID, type, start and end times, progress, and resources duration.

```tsx
function nodeDuration(node: models.NodeStatus, now: moment.Moment) {
    const endTime = node.finishedAt ? moment(node.finishedAt) : now;
    return endTime.diff(moment(node.startedAt)) / 1000;
}

// Iterate over the node's subtree and find pod in error or fail
function failHosts(node: models.NodeStatus, workflow: models.Workflow) {
    const hosts = new Array<string>();
    const toVisit = [node.id];
    while (toVisit.length > 0) {
        const nodeNameToVisit = toVisit[toVisit.length - 1];
        toVisit.pop();

        if (nodeNameToVisit in workflow.status.nodes) {
            const nodeToVisit = workflow.status.nodes[nodeNameToVisit];
            if (
                nodeToVisit.type === 'Pod' &&
                (nodeToVisit.phase === models.NODE_PHASE.FAILED || nodeToVisit.phase === models.NODE_PHASE.ERROR) &&
                hosts.indexOf(nodeToVisit.hostNodeName) === -1
            ) {
                hosts.push(nodeToVisit.hostNodeName);
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
