# Select Promotion

Fired when a user selects a promotion out of a list. It is surfaced in promotion reports to report on which promotions were selected out of those viewed.

## Javascript Code

```js
window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: "select_promotion",
  eventModel: {
    items: "<items>",

    // Omit these if they are set at the item level
    creative_name: "Summer Banner",
    creative_slot: "featured_app_1",
    location_id: "ChIJIQBpAG2ahYAR_6128GcTUEo",
    promotion_id: "P_12345",
    promotion_name: "Summer Sale",

    // Send these parameters if the promotion was in a list
    list_type: "<list_type>",

    // Send these parameters if the promotion showed up in a search (list_type="search_results")
    facets: "<facets>",
    search_term: "<search_term>",
    search_type: "<search_type>",
  }
});
```

## Variable Definitions

|Field|Type|Required|Description|Example|Pattern|Min Length|Max Length|Minimum|Maximum|Multiple Of|
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|creative_name|string|recommended if not set at item level|The name of a creative used in a promotional spot.|summer_banner2|
|creative_slot|string|recommended if not set at item level|The name of a creative slot.|carousel1|
|facets|delimited string|contextual|A double-delimited string of key/value pairs representing the refinements that were applied to this search. Only set if the list type is a search result or filter_by_group.|category:skin_health~skin_concern:acne~featured_as:best_seller|
|list_type|string|contextual|The type of list the item was found in.|cards, carousel, popular_products, search_results|
|promotion_id|string|Either `promotion_id` or `promotion_name` is recommended if not set at item level|The ID of a product promotion.|P_12345|
|promotion_name|string|Either `promotion_id` or `promotion_name` is recommended if not set at item level|The name of a product promotion. One of `promotion_id` or `promotion name` is required.|Summer 15OFF|
|search_term|string|contextual|The final search term submitted after any correction has been performed. Only set if the `list_type` is `search_results`.|sunscreen|
|search_type|string|contextual|The type of search performed. Only set if the `list_type` is `search_results`.|site, filter_by_group|
|items|array of [items](/schemas/item.md)|required|Populate with item objects that represent the product viewed.|`[{item_id: "SKU_12345", item_name: "Stan and Friends Tee", affiliation: "Google Merchandise Store", coupon: "SUMMER_FUN", currency: "USD", discount: 2.22, index: 0, item_brand: "Google", item_category: "Apparel", item_category2: "Adult", item_category3: "Shirts", item_category4: "Crew", item_category5: "Short sleeve", item_list_id: "carousel", item_list_name: "Carousel", item_variant: "green", location_id: "ChIJIQBpAG2ahYAR_6128GcTUEo", price: 9.99, quantity: 1}]`
