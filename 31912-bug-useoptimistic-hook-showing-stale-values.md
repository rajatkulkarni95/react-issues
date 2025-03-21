# Bug: useOptimistic hook showing stale values

> Issue #31912 - Created on 12/26/2024

> Original URL: https://github.com/facebook/react/issues/31912

## Description


React version: "^18" I tried on "^18.3.1" as well
![image](https://github.com/user-attachments/assets/bf830eaa-182a-4562-96c4-2c03f30d8750)
![image](https://github.com/user-attachments/assets/7ae48ac0-f08b-4bcc-9226-a54361fe44d1)



## The current behavior
Number and button appears for like 0.1 second  and then dissapears
first i had this setup with database and little more complex ui then i reduced it to very simple arrays with number and button 
Btw i did try this with useTransition as well neither that neither action works


## The expected behavior
Number with button should appear without dissapearing 

