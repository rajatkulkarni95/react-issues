# Bug: Not able assign React query fetched data to nested array (nothing but table Row) in react with Typescript app

> Issue #29676 - Created on 5/31/2024

> Original URL: https://github.com/facebook/react/issues/29676

## Description

<!--
The live code example with following link : https://stackblitz.com/edit/ashok-reddy?file=muitable.tsx
-->

React version:
react : 18.2

## Steps To Reproduce

1.
2.

<!--
   await mutateAsync(
      { dataWithDisplayOrder },
      {
        onSuccess: (responseid: any) => {
          //  i got response as id
          setResponseId(responseid);
          // here restting the nestedArray
          resetField('nestedArray');

          // now here i'm passing this id to to fetch the saved details using useeffect
          setResponseId(responseid);
          // here is my ask ???????
          /// My asK here is how to set fetched data to nestedArray??? to display in UI
        },
        onError: (error) => {},
      }
    );
  };

-->

Link to code example: https://stackblitz.com/edit/ashok-reddy?file=muitable.tsx

<!--
 
  ehttps://stackblitz.com/edit/ashok-reddy?file=muitable.tsx
-->

## 
Not able assign React query fetched data to nested array (nothing but table Row) in react with Typescript app

## How to query fetched data to nested array (nothing but table Row)

