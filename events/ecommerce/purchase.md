# Purchase

Fired when a user completes a purchase. This can include purchase of physical or digital goods, registering for a conference, making a donation, or any other exchange of value.

## Javascript Code

```js

window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: "purchase",
  eventModel: {
    affiliation: "<affiliation>", 
    count_purchase: 1,
    coupon: "<coupon>", 
    currency: "<currency>", 
    items: "<items>", 
    shipping: "<shipping>", 
    tax: "<tax>", 
    transaction_id: "<transaction_id>", 
    value: "<value>" 
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|affiliation|string|recommended|A product affiliation to designate a supplying company or brick and mortar store location. Event-level and item-level affiliation parameters are independent.|`Google Merchandise Store`|`^[A-Za-z0-9_]+$`|
|coupon|string|recommended|The coupon name/code associated with the event. Event-level and item-level coupon parameters are independent.|`25OFF`|`^[A-Za-z0-9_]+$`|
|currency|string|required|Currency of the items associated with the event, in 3-letter ISO 4217 format.|`USD`|`^[A-Z]{3}$`|3|3|
|items|array of [items](/schemas/item.md)|required|Populate with [item](/schemas/item.md) objects that represent the product(s) purchased.|`[{item_id: "SKU_12345", item_name: "Stan and Friends Tee", affiliation: "Google Merchandise Store", coupon: "SUMMER_FUN", currency: "USD", discount: 2.22, index: 0, item_brand: "Google", item_category: "Apparel", item_category2: "Adult", item_category3: "Shirts", item_category4: "Crew", item_category5: "Short sleeve", item_list_id: "related_products", item_list_name: "Related Products", item_variant: "green", location_id: "ChIJIQBpAG2ahYAR_6128GcTUEo", price: 9.99, quantity: 1 }, { item_id: "SKU_12346", item_name: "Google Grey Women's Tee", affiliation: "Google Merchandise Store", coupon: "SUMMER_FUN", currency: "USD", discount: 3.33, index: 1, item_brand: "Google", item_category: "Apparel", item_category2: "Adult", item_category3: "Shirts", item_category4: "Crew", item_category5: "Short sleeve", item_list_id: "related_products", item_list_name: "Related Products", item_variant: "gray", location_id: "ChIJIQBpAG2ahYAR_6128GcTUEo", price: 20.99, promotion_id: "P_12345", promotion_name: "Summer Sale", quantity: 1}]`
|shipping|number|recommended|Shipping cost associated with a transaction.|`3.33`|`^\d+\.\d\d$`|||0.00|
|tax|number|recommended|Tax cost associated with a transaction.|`1.11`|`^\d+\.\d\d$`|||0.00|
|transaction_id|string|required|The unique identifier of a transaction.|`T12345`|
|value|number|required|The monetary value of the event.|`7.77`|`^\d+\.\d\d$`|||0.00|