# forceUpdate not work in child component GuardGraph 

> Issue #31019 - Created on 9/22/2024

> Original URL: https://github.com/facebook/react/issues/31019

## Description

```
export default function GuardSetting (props:any) {
  const [, forceUpdate] = useReducer(x => x + 1, 0);

    return (
      <Paper sx={{ width: '100%', pt:'1em', }} >
        <SettingHeader name={'Launch Guard'}/>
        <ReactFlowProvider>
          <GuardGraph {...props} forceUpdate={forceUpdate}/>
        </ReactFlowProvider>
      </Paper>
    );
}
```

Is there any more elegant way to refresh GuardGraph without using window.location.reload()?
Thx.

