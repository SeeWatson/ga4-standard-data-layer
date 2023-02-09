# Item Object

An `item` is how GA4 refers to a product.  An item object should be sent whenever a product is displayed, selected, added to a cart, or purchased.

## Object format

```json
{
  // Required - set both of these every time an item occurs in the items array
  "item_id": "<item_id>",
  "item_name": "<item_name>",

  // Global - always set these if the data is available
  "affiliation": "<affiliation>",
  "currency": "<currency>",
  "item_brand": "<item_brand>",
  "item_category": "<item_category>",
  "item_variant": "<item_variant>",
  "price": "<price>",
  "quantity": "<quantity>",

  // Contextual - only set these if the product is discounted or if the user applies a coupon
  "coupon": "<coupon>",
  "discount": "<discount>",

  // Contextual - if a product shows up in a list, include these on the view_item_list event. If the product is selected out of the list, include these parameterts on all subsequent events (select_item, view_item, add_to_cart, ..., purchase) to serve as item finding method
  "item_list_id": "<item_list_id>",
  "item_list_name": "<item_list_name>",

  // Contextual - only set these on view_promotion and select_promotion events
  "creative_name": "<creative_name>",
  "creative_slot": "<creative_slot>",
  "promotion_id": "<promotion_id>",
  "promotion_name": "<promotion_name>",

  // Contextual - only set if the item represents a location (booking a hotel)
  "location_id": "<location_id>",
}
```

## Variable definitions
|Name|Type|Required|Description|Example Value|
| --- | --- | --- | --- | --- |
|affiliation|string|recommended|A product affiliation to designate a supplying company or brick and mortar store location.|Google Store|
|coupon|string|contextual|Coupon code used for a purchase.|25OFF|
|creative_name|string|recommended if item is being sent with a promotion event and not set at the event level|The name of a creative used in a promotional spot.|summer_banner2|
|creative_slot|string|recommended if item is being sent with a promotion event and not set at the event level|The name of a creative slot.|featured_app_1|
|currency|string|recommended|The currency, in 3-letter ISO 4217 format.|USD|
|discount|number|conditional|Monetary value of discount associated with a purchase.|2.22|
|index|integer|conditional|The numerical index of the item position (1-indexed). If this is the 3rd card in a single row of promotions, send `3`. If this product is the 5th result in a set of product search results, you would send `5` here. If this is the 2nd item in the 3rd row of a 3-up card layout, send `8` (3 + 3 + 2).|5|
|item_brand|string|recommended|Item brand|Google|
|item_category|string|recommended|Item Category (context-specific). `item_category2` through `item_category5`can also be used if the item has many categories.|Apparel|
|item_id|string|required|Item ID (context-specific).|SKU_12345|
|item_list_id|string|contextual|The computer-readable machine name of the list the item showed up in (if sent with a view_item_list event). Use UUID provided by the component if no more specific ID is available.|12345abcde12345|
|item_list_name|string|contextual|The human-readable name of the item list the item showed up in (if sent with a view_item_list event). If one is not available, populate with numerical index of which list this is on the page (1-indexed). For `filter_by_group` component, use that value.|filter_by_group, recommended_products, recently_viewed_products|
|item_name|string|required|Item Name (context-specific).|green triangle widget|
|item_subscription_type|string|recommended|Item Subscription Type. The subscription type when a user chooses to subscribe to a product being sent multiple times after their purchase.|3-months, 6-months, 9-months|
|item_variant|string|recommended|The variant of the item.|Black|
|location_id|string|recommended if the item is associated with a physical location|The location associated with the event. If possible, set to the Google Place ID that corresponds to the associated item. Can also be overridden to a custom location ID string.|L_12345|
|price|number|recommended|The monetary price of the item, in units of the specified currency parameter.|9.99|
|promotion_id|string|Either `promotion_id` or `promotion_name` is required if item is being sent with a promotion event and one of these is not set at the event level|The ID of a product promotion.|P_12345|
|promotion_name|string|Either `promotion_id` or `promotion_name` is required if item is being sent with a promotion event and one of these is not set at the event level|The name of a product promotion. One of `promotion_id` or `promotion name` is required.|Summer Sale|
|quantity|integer|recommended|Item quantity.|1|