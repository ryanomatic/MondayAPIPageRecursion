# Monday API Items Recursion for Power BI / PowerQuery
PowerBI Solution for recursively loading data from Monday.com with cursor pagination for API v2024-01.

## Help needed:
Is it possible to pass null values into PowerQuery functions? Not a practical problem but not an elegant solution since we can simply pass "new" instead. If you know how to do this, please let me know/merge in your changes.

## What?
Monday API version 2023-10 introduced pagination to items (limite 500), breaking simple 'pull all data' queries. Most of the current solutions today solve this problem by manually writing in query to pull the first 500, second 500, etc. This is problematic if your data is growing as it won't continue to add items as your data grows. This example/solution will dynamically pull all the data.

## Helpful Links
> 1) [Monday - Migrating to new API](https://developer.monday.com/api-reference/docs/migrating-to-v-2023-10)
> 2) [Monday - GraphQL sandbox](https://monday.com/developers/v2/try-it-yourself)
> 3) [Monday - Items_Page & Next_Items (GraphQL example)](https://developer.monday.com/api-reference/docs/items_page)
> 4) [Recursion in Power BI](https://www.thepoweruser.com/2019/07/01/recursive-functions-in-power-bi-power-query/)

## How does it work
When getting data from Monday's API, it will return the data as well as a cursor which is the next subset of data. The function grabs data either starting with a fresh query or using a cursor. If there is no additional cursor, it will return the data it received. If there is a cursor, it will call itself again (with the new cursor) and append the returned data together. This continues forever until the end of data is found, your computer runs out of memory, or a recursion limit is hit (never seen it, even using tiny batch sizes).  

## Instructions
1) Create 'APIKey' function with your Monday API Key
* Other options: Write directly into function, query from database or other secure source, basic query <ins>(If as query, do not let it load or you could leak the key!)</ins>
3) Create the function "Fn_RecursiveMondayItems"
* Name it whatever you want
  
3) Invoke the function using the parameters below
   * Board = The BoardID you're getting items for, this is numeric.
   * InitialCursor = "new" will indicate the start of data
     
4) Transform data, you'll probably want to pivot it - example is included in this repo
