# View Item

Fired when a user views a specific product. Typically fired on views of a dedicated product detail page, whereas view_item_list is fired on listing pages. However, if a page contains multiple items in a non-listing format (variants of the same product selected via an on-page component) this event could be fired multiple times to represent viewing each of the individual products.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: "view_item",
  eventModel: {
    count_view_item: 1,
    currency: "<currency>", 
    items: "<items>", 
    value: "<value>" 
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|currency|string|recommended|Currency of the items associated with the event, in 3-letter ISO 4217 format.|USD|^[A-Z]{3}$|3|3|
|items|array of [items](/schemas/item.md)|required|Populate with item objects that represent the product viewed.|`[{item_id: "SKU_12345", item_name: "Stan and Friends Tee", affiliation: "Google Merchandise Store", coupon: "SUMMER_FUN", currency: "USD", discount: 2.22, index: 0, item_brand: "Google", item_category: "Apparel", item_category2: "Adult", item_category3: "Shirts", item_category4: "Crew", item_category5: "Short sleeve", item_list_id: "related_products", item_list_name: "Related Products", item_variant: "green", location_id: "ChIJIQBpAG2ahYAR_6128GcTUEo", price: 9.99, quantity: 1}]`
|value|number|recommended|The monetary value of the event.|`7.77`|^\d+\.\d\d$|||0.00|