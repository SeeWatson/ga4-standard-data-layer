# Select Content

Fired when a user selects a non-product item out of a list.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: "select_content",
  eventModel: {
    count_select_content: 1,
    identifier: "<identifier>",
    facets: "<facets>",
    index: "<index>",
    item_list_id: "<item_list_id>", 
    item_list_name: "<item_list_name>", 
    list_type: "<list_type>", 
    search_term: "<search_term>", 
    search_type: "<search_type>", 
  }
});
```

## Variable Definitions
|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|facets|delimited string|contextual|A double-delimited string of key/value pairs representing the refinements that were applied.|`category:Apparel~variant:green~featured_as:best_seller`|
|identifier|string|recommended|The machine-readable content ID. This should be a unique value specific to this content item, if one exists. If one does not exist, this can also be populated with the same value as the `<name>`.|12345|
|index|integer|required|The numerical index of the item position (1-indexed). For instance, if this is the 5th search result, you would send 5 here. If this is the 3rd card in a single row, send 3. If this is the 2nd item in the 3rd row of a 3-up card layout, send 8 (3 + 3 + 2).|`5`|
|item_list_id|string|recommended|The computer-readable machine name of the list the item showed up in. Use UUID provided by the component if no more specific ID is available.|`12345abcde12345`|
|item_list_name|string|recommended|The human-readable name of the list the item showed up in. If one is not available, populate with numerical index of which list this is on the page (1-indexed).|`recommended_products, recently_viewed_products, search_results`|
|list_type|string|contextual|The type of list the item was found in.|`cards, search_results`|
|name|string|recommended|The human-readable content name. This should be something that an analyst without a deep knowledge of the technical implementation of the site can easily identify the content item with. It should be in regular sentence case or capital case.|"About Us"|
|search_term|string|contextual|The final search term submitted after any correction has been performed. Only set if the `list_type` is `search_results`.|`shirts`|
|search_type|string|contextual|The type of search performed. Only set if the `list_type` is `search_results`.|`site,product,global`|