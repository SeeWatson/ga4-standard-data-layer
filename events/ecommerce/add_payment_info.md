# Add Payment Info

Fired when a user adds payment information during a checkout flow.

## Javascript Code

```js
window.dataLayer = window.dataLayer || [];
dataLayer.push({
  event: "add_payment_info",
  eventModel: {
    count_add_payment_info: 1,
    coupon: "<coupon>", 
    currency: "<currency>", 
    items: "<items>", 
    payment_type: "<payment_type>", 
    value: "<value>" 
  }
});
```

## Variable Definitions

|Parameter|Type|Required|Description|Example|Pattern|Min Length|Max Length|
| --- | --- | --- | --- | --- | --- | --- | --- |
|coupon|string|recommended|The coupon name/code associated with the event. Event-level and item-level coupon parameters are independent.|`25OFF`|`^[A-Za-z0-9_]+$`|
|currency|string|recommended|Currency of the items associated with the event, in 3-letter ISO 4217 format.|`USD`|`^[A-Z]{3}$`|3|3|
|items|array of [items](/schemas/item.md)|required|Populate with item objects that represent the product viewed.|`[{item_id: "SKU_12345", item_name: "Stan and Friends Tee", affiliation: "Google Merchandise Store", coupon: "SUMMER_FUN", currency: "USD", discount: 2.22, index: 0, item_brand: "Google", item_category: "Apparel", item_category2: "Adult", item_category3: "Shirts", item_category4: "Crew", item_category5: "Short sleeve", item_list_id: "related_products", item_list_name: "Related Products", item_variant: "green", location_id: "ChIJIQBpAG2ahYAR_6128GcTUEo", price: 9.99, quantity: 1}]`|
|payment_type|string|recommended|The chosen method of payment.|`credit_card`|`^[a-z_]+$`|
|value|number|recommended|The monetary value of the event.|`7.77`|`^\d\.\d\d$`|||0.00|