---
title: Exploring Shared Components
---
# Exploring Shared Components

Components are reusable UI elements that encapsulate specific functionality or display logic. They are used to build the user interface by combining them in various ways to create complex layouts and interactions. Components in the `Shared` directory are designed to be used across different parts of the application, promoting code reuse and consistency.

<SwmSnippet path="/ui/src/app/shared/components/object-editor.tsx" line="150">

---

## Examples of Components

This component provides a link to learn how to get <SwmToken path="ui/src/app/shared/components/object-editor.tsx" pos="150:35:37" line-data="                    &lt;a href=&#39;https://argo-workflows.readthedocs.io/en/latest/ide-setup/&#39;&gt;Learn how to get auto-completion in your IDE.&lt;/a&gt;">`auto-completion`</SwmToken> in your IDE.

```tsx
                    <a href='https://argo-workflows.readthedocs.io/en/latest/ide-setup/'>Learn how to get auto-completion in your IDE.</a>
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/shared/components/timestamp.tsx" line="6">

---

This component imports and uses the <SwmToken path="ui/src/app/shared/components/timestamp.tsx" pos="6:2:2" line-data="import useTimestamp, {TIMESTAMP_KEYS} from &#39;../use-timestamp&#39;;">`useTimestamp`</SwmToken> hook and <SwmToken path="ui/src/app/shared/components/timestamp.tsx" pos="6:6:6" line-data="import useTimestamp, {TIMESTAMP_KEYS} from &#39;../use-timestamp&#39;;">`TIMESTAMP_KEYS`</SwmToken>.

```tsx
import useTimestamp, {TIMESTAMP_KEYS} from '../use-timestamp';
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/shared/components/graph/graph-panel.tsx" line="23">

---

This component includes a property <SwmToken path="ui/src/app/shared/components/graph/graph-panel.tsx" pos="23:1:1" line-data="    storageScope: string; // the scope of storage, similar graphs should use the same vaulue">`storageScope`</SwmToken> to manage the scope of storage for similar graphs.

```tsx
    storageScope: string; // the scope of storage, similar graphs should use the same vaulue
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/shared/components/first-time-user-panel.tsx" line="4">

---

This component wraps children components in a First Time User (FTU) panel to provide explanations on how to use the feature.

```tsx
// This wraps the children components in a FTU which allows you to provide an explanation of how to use the feature.
```

---

</SwmSnippet>

### Visual Elements

Visual elements such as icons, buttons, and panels are designed to provide a consistent look and feel across the application. Icons are used to represent actions or objects visually, buttons trigger actions when clicked, and panels are used to group related content together. These elements are implemented using React and styled to match the application's design guidelines.

### Functional Elements

Functional elements like data parsers and loaders handle specific tasks within the application. Data parsers process and transform data into a usable format, while loaders manage the loading state of components, providing feedback to users during data fetching operations. These elements ensure that the application remains responsive and user-friendly.

## Component Endpoints

Endpoints of Components

<SwmSnippet path="/ui/src/app/shared/components/object-editor.tsx" line="51">

---

### fetch

The <SwmToken path="ui/src/app/shared/components/object-editor.tsx" pos="53:9:9" line-data="                const res = await fetch(uri);">`fetch`</SwmToken> function is used to retrieve the JSON schema from the specified URI. This schema is then used to provide <SwmToken path="ui/src/app/shared/components/object-editor.tsx" pos="150:35:37" line-data="                    &lt;a href=&#39;https://argo-workflows.readthedocs.io/en/latest/ide-setup/&#39;&gt;Learn how to get auto-completion in your IDE.&lt;/a&gt;">`auto-completion`</SwmToken> and validation for JSON inputs in the editor.

```tsx
            const uri = uiUrl('assets/jsonschema/schema.json');
            try {
                const res = await fetch(uri);
                const swagger = await res.json();
```

---

</SwmSnippet>

<SwmSnippet path="/ui/src/app/shared/components/object-editor.tsx" line="58">

---

### <SwmToken path="ui/src/app/shared/components/object-editor.tsx" pos="58:7:7" line-data="                languages.json.jsonDefaults.setDiagnosticsOptions({">`setDiagnosticsOptions`</SwmToken>

The <SwmToken path="ui/src/app/shared/components/object-editor.tsx" pos="58:7:7" line-data="                languages.json.jsonDefaults.setDiagnosticsOptions({">`setDiagnosticsOptions`</SwmToken> function configures the Monaco editor to enable JSON validation and <SwmToken path="ui/src/app/shared/components/object-editor.tsx" pos="150:35:37" line-data="                    &lt;a href=&#39;https://argo-workflows.readthedocs.io/en/latest/ide-setup/&#39;&gt;Learn how to get auto-completion in your IDE.&lt;/a&gt;">`auto-completion`</SwmToken> based on the fetched schema. This enhances the user experience by providing real-time feedback and suggestions while editing JSON.

```tsx
                languages.json.jsonDefaults.setDiagnosticsOptions({
                    validate: true,
                    schemas: [
                        {
                            uri,
                            fileMatch: ['*'],
                            schema: {
                                $id: 'http://workflows.argoproj.io/' + type + '.json',
                                $ref: '#/definitions/' + type,
                                $schema: 'http://json-schema.org/draft-07/schema',
                                definitions: swagger.definitions
                            }
                        }
                    ]
                });
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
