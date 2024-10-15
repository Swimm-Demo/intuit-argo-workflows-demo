---
title: User Interface Overview
---
# User Interface Overview

The User Interface (UI) is responsible for displaying user-related information and interactions. It includes components such as <SwmToken path="ui/src/app/userinfo/user-info.tsx" pos="12:4:4" line-data="export function UserInfo() {">`UserInfo`</SwmToken>, which fetches and displays user details like issuer, subject, groups, name, email, and service account information. The UI provides a structured and user-friendly way to present user information, including login/logout functionality and help documentation.

# <SwmToken path="ui/src/app/userinfo/user-info.tsx" pos="12:4:4" line-data="export function UserInfo() {">`UserInfo`</SwmToken> Component

The <SwmToken path="ui/src/app/userinfo/user-info.tsx" pos="12:4:4" line-data="export function UserInfo() {">`UserInfo`</SwmToken> component is a key part of the UI that fetches user data using the <SwmToken path="ui/src/app/userinfo/user-info.tsx" pos="19:13:13" line-data="                const newUserInfo = await services.info.getUserInfo();">`getUserInfo`</SwmToken> function and updates the UI with user details. This component ensures that user information such as issuer, subject, groups, name, email, and service account information is displayed accurately.

<SwmSnippet path="/ui/src/app/userinfo/user-info.tsx" line="12">

---

The <SwmToken path="ui/src/app/userinfo/user-info.tsx" pos="12:4:4" line-data="export function UserInfo() {">`UserInfo`</SwmToken> component fetches user data using the <SwmToken path="ui/src/app/userinfo/user-info.tsx" pos="19:13:13" line-data="                const newUserInfo = await services.info.getUserInfo();">`getUserInfo`</SwmToken> function and updates the UI with user details. Error handling is integrated to notify users of any issues during data retrieval.

```tsx
export function UserInfo() {
    const [error, setError] = useState<Error>(null);
    const [userInfo, setUserInfo] = useState<GetUserInfoResponse>();

    useEffect(() => {
        (async function getUserInfoWrapper() {
            try {
                const newUserInfo = await services.info.getUserInfo();
                setUserInfo(newUserInfo);
                setError(null);
            } catch (newError) {
                setError(newError);
            }
        })();
    }, []);

    return (
        <Page title='User Info' toolbar={{breadcrumbs: [{title: 'User Info'}]}}>
            <ErrorNotice error={error} />
            <Notice>
                <h3>
```

---

</SwmSnippet>

# Error Handling

Error handling is integrated into the <SwmToken path="ui/src/app/userinfo/user-info.tsx" pos="12:4:4" line-data="export function UserInfo() {">`UserInfo`</SwmToken> component to notify users of any issues during data retrieval. This ensures that users are informed of any problems and can take appropriate action.

# Displaying User Information

The <SwmToken path="ui/src/app/userinfo/user-info.tsx" pos="12:4:4" line-data="export function UserInfo() {">`UserInfo`</SwmToken> component displays user details like issuer and subject if the <SwmToken path="ui/src/app/userinfo/user-info.tsx" pos="14:4:4" line-data="    const [userInfo, setUserInfo] = useState&lt;GetUserInfoResponse&gt;();">`userInfo`</SwmToken> object is available. This ensures that relevant user information is presented to the user in a clear and organized manner.

<SwmSnippet path="/ui/src/app/userinfo/user-info.tsx" line="35">

---

The <SwmToken path="ui/src/app/userinfo/user-info.tsx" pos="12:4:4" line-data="export function UserInfo() {">`UserInfo`</SwmToken> component conditionally renders user details such as issuer and subject if they are available in the <SwmToken path="ui/src/app/userinfo/user-info.tsx" pos="35:2:2" line-data="                {userInfo &amp;&amp; (">`userInfo`</SwmToken> object.

```tsx
                {userInfo && (
                    <>
                        {userInfo.issuer && (
                            <dl>
                                <dt>Issuer:</dt>
                                <dd>{userInfo.issuer}</dd>
                            </dl>
                        )}
                        {userInfo.subject && (
                            <dl>
```

---

</SwmSnippet>

# User APIs

The UI interacts with several user APIs to fetch and manage user information. These APIs include <SwmToken path="ui/src/app/userinfo/user-info.tsx" pos="19:13:13" line-data="                const newUserInfo = await services.info.getUserInfo();">`getUserInfo`</SwmToken> and <SwmToken path="ui/src/app/shared/services/info-service.ts" pos="24:1:1" line-data="    collectEvent(name: string) {">`collectEvent`</SwmToken>.

## <SwmToken path="ui/src/app/userinfo/user-info.tsx" pos="19:13:13" line-data="                const newUserInfo = await services.info.getUserInfo();">`getUserInfo`</SwmToken>

The <SwmToken path="ui/src/app/userinfo/user-info.tsx" pos="19:13:13" line-data="                const newUserInfo = await services.info.getUserInfo();">`getUserInfo`</SwmToken> function retrieves user information from the backend. It sends a GET request to the <SwmPath>[ui/src/app/userinfo/](ui/src/app/userinfo/)</SwmPath> endpoint and returns the user details such as issuer, subject, groups, name, email, and service account information.

<SwmSnippet path="/ui/src/app/shared/services/info-service.ts" line="20">

---

The <SwmToken path="ui/src/app/shared/services/info-service.ts" pos="20:1:1" line-data="    getUserInfo() {">`getUserInfo`</SwmToken> function sends a GET request to the <SwmPath>[ui/src/app/userinfo/](ui/src/app/userinfo/)</SwmPath> endpoint and returns the user details.

```typescript
    getUserInfo() {
        return requests.get(`api/v1/userinfo`).then(res => res.body as GetUserInfoResponse);
    },
```

---

</SwmSnippet>

## <SwmToken path="ui/src/app/shared/services/info-service.ts" pos="24:1:1" line-data="    collectEvent(name: string) {">`collectEvent`</SwmToken>

The <SwmToken path="ui/src/app/shared/services/info-service.ts" pos="24:1:1" line-data="    collectEvent(name: string) {">`collectEvent`</SwmToken> function is used to send user interaction events to the backend. It sends a POST request to the <SwmPath>[pkg/apiclient/event/](pkg/apiclient/event/)</SwmPath> endpoint with the event name as the payload.

<SwmSnippet path="/ui/src/app/shared/services/info-service.ts" line="24">

---

The <SwmToken path="ui/src/app/shared/services/info-service.ts" pos="24:1:1" line-data="    collectEvent(name: string) {">`collectEvent`</SwmToken> function sends a POST request to the <SwmPath>[pkg/apiclient/event/](pkg/apiclient/event/)</SwmPath> endpoint with the event name as the payload.

```typescript
    collectEvent(name: string) {
        return requests.post(`api/v1/tracking/event`).send({name});
    }
```

---

</SwmSnippet>

&nbsp;

*This is an auto-generated document by Swimm 🌊 and has not yet been verified by a human*

<SwmMeta version="3.0.0" repo-id="Z2l0aHViJTNBJTNBaW50dWl0LWFyZ28td29ya2Zsb3dzLWRlbW8lM0ElM0FTd2ltbS1EZW1v" repo-name="intuit-argo-workflows-demo"><sup>Powered by [Swimm](/)</sup></SwmMeta>
