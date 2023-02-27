1. Query:<br/>

```
{
  test_alarms(
    luceneFilter: "3c50a87291707504aa000000000000000000000045"
    filter: {key: systemId}
    sort: [{ field:id,order: desc }]
    limit: { size: 5, offset: 0 }
  ) {
 		items {
 		  id
 		  consoleUri
 		  type
 		  resourceUri
 		}
    total
    pageLimit
  }
```

2. Mutation: <br/>
  
  ```
  {
  human(id: "1000") {
    name
    height
  }
}
  ```
