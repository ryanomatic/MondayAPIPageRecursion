# Monday API Page Recursion with Power BI Query
PowerBI Solution for recursively loading data from Monday.com with cursor pagination.

## What?
Monday API version 2023-10 introduced pagination to items (limite 500), breaking simple 'pull all data' queries. Most of the current solutions today solve this problem by manually writing in query to pull the first 500, second 500, etc. This is problematic if your data is growing as it won't continue to add items as your data grows. This example/solution will dynamically pull all the data.

## Helpful Links
> 1) [Monday - Migrating to new API](https://developer.monday.com/api-reference/docs/migrating-to-v-2023-10)
> 2) [Monday - Items_Page & Next_Items (GraphQL example)](https://developer.monday.com/api-reference/docs/items_page)
> 3) [Recursion in Power BI](https://www.thepoweruser.com/2019/07/01/recursive-functions-in-power-bi-power-query/)

## How does it work
When getting data from Monday's API, it will return the data as well as a cursor which is the next subset of data. We will create a function that takes the BoardID and Cursor as input and returns the resulting data. If the cursor indicates the end of the data, we append all the data together and return it. If the cursor indicates another page, we call this function (recursion) using the next item cursor and append its results to the ones we just found.

## Instructions

