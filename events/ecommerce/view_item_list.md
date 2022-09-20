# View Item List

Fired when a user views a list of products.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: "view_item_list",
  eventModel: {
    count_view_item_list: 1,
    facets: "<facets>", 
    items: "<items>", 
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
|items|array of [items](/schemas/item.md)|recommended|Populate with item objects that represent each product in the list.|`[{item_id: "SKU_12345", item_name: "Stan and Friends Tee", affiliation: "Google Merchandise Store", coupon: "SUMMER_FUN", currency: "USD", discount: 2.22, index: 0, item_brand: "Google", item_category: "Apparel", item_category2: "Adult", item_category3: "Shirts", item_category4: "Crew", item_category5: "Short sleeve", item_list_id: "related_products", item_list_name: "Related Products", item_variant: "green", location_id: "ChIJIQBpAG2ahYAR_6128GcTUEo", price: 9.99, quantity: 1}]`
|item_list_id|string|recommended|The computer-readable machine name of the list the item showed up in. Use UUID provided by the component if no more specific ID is available.|`12345abcde12345`|
|item_list_name|string|recommended|The human-readable name of the list the item showed up in. If one is not available, populate with numerical index of which list this is on the page (1-indexed).|`recommended_products, recently_viewed_products, search_results`|
|list_type|string|contextual|The type of list the item was found in.|`cards, search_results`|
|search_term|string|contextual|The final search term submitted after any correction has been performed. Only set if the `list_type` is `search_results`.|`shirts`|
|search_type|string|contextual|The type of search performed. Only set if the `list_type` is `search_results`.|`site,product,global`|