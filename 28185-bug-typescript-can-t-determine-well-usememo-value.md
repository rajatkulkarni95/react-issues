# Bug: typescript can't determine well useMemo value

> Issue #28185 - Created on 2/1/2024

> Original URL: https://github.com/facebook/react/issues/28185

## Description

React version: `18.2.0`
TypeScript version: `5.0.2`

## The expected behavior
```js
  const shouldNotRender = useMemo(() => !organization || !ehrUser, [organization, ehrUser]);
  // if (!organization || !ehrUser) return null;

  if (shouldNotRender) return null;

  return (
    <UserManagement
      showNotification={showUserManagementNotification}
      user={{ ...ehrUser, organization }}
      onRolesChanged={onRolesChanged}
    />
  );
```
### Error
<img width="758" alt="Screenshot 2024-02-01 at 14 42 59" src="https://github.com/facebook/react/assets/22234568/503d5d0c-f2d6-4646-bd24-da61e6686502">


## The current behavior
```js
  // const shouldNotRender = useMemo(() => !organization || !ehrUser, [organization, ehrUser]);
  if (!organization || !ehrUser) return null;

  // if (shouldNotRender) return null;

  return (
    <UserManagement
      showNotification={showUserManagementNotification}
      user={{ ...ehrUser, organization }}
      onRolesChanged={onRolesChanged}
    />
  );
```
### No error
<img width="714" alt="Screenshot 2024-02-01 at 14 43 32" src="https://github.com/facebook/react/assets/22234568/b3615f5c-3195-4a32-9617-6165b92d5c8e">

