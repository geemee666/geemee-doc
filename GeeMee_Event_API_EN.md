# GeeMee Event API【EN】

The Event API provides advertisers running web-based advertisements with a secure server-to-server interface. By sending conversion events to GeeMee's (hereinafter referred to as "we", "us", or "our") designated endpoint, advertisers can directly share user-triggered events from their websites. This enables us to gain comprehensive insights into visitor behavior, thereby optimizing ad campaign performance.

## 1. Advantages of Event API

1. **No Page Code Insertion Required**: Unlike Pixel-based solutions, Event API eliminates the need to embed code in web pages. Simply construct the payload and send it to our endpoint.
2. **Cross-Domain Tracking Support**:
    - Pixel cannot track user journeys spanning domains beyond the advertiser’s own. Event API enables cross-domain event reporting.
    - Example: Brazil’s popular *boleto* payment method involves generating an online barcode for offline payment—a scenario where Pixel fails. Event API can reliably report such payment events.
1. **Multi-Page Application (MPA) Compatibility**: Event API supports event reporting in MPAs where Pixel may face limitations.

## 2. Using Event API

### Request URL

`https://s.geemee.ai/e/s2s`

> **Note**: Only `POST` requests are supported. Requests must be initiated from your server, and server logs should record callback activities.

### Whitelist Configuration

**Provide your server IP(s) to GeeMee before launch. Requests from non-whitelisted IPs will be rejected.**

### Headers

`Content-Type: application/json`

### Request Parameters

| **Parameter**    | **Required** | **Type** | **Description**                                                                                                                               |
| ---------------- | ------------ | -------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| `eid`            | Y            | string   | Event name                                                                                                                                    |
| `pixel_click_id` | Y            | string   | Pass-through parameter; unique `click_id` appended to the URL when a user clicks an ad and lands on your site. Capture and return this value. |
| `pixel_id`       | Y            | string   | Unique ID assigned by our platform to your website/app.                                                                                       |
| `data`           | Y            | JSON     | Event-specific attributes                                                                                                                     |
| `ip`             | Y            | string   | User IP address                                                                                                                               |

### Request Example

```json
{
  "eid": "EVENT_CONTENT_VIEW",
  "pixel_click_id": "0_0_1t5lia_6Nx_2YH_6kW_0_5md7hw6Qi0m6p105dTsOyV",
  "pixel_id": "12345",
  "data": {
    "content_id": "111111",
    "content_type": "vip",
    "content_name": "Premium Subscription",
    "value": "9.9",
    "currency": "USD",
    "price": "1"
  },
  "ip": "106.215.139.186"
}
```

### Status Codes

An HTTP `200 OK` response indicates a successful API call.

## 3. Web Events & Attributes

### Standard Web Events

Use our predefined standard events to maximize campaign optimization. Select the most relevant event name for user actions:

| ​**Event Name**​                | ​**Description**​                              |
| ------------------------------- | ---------------------------------------------- |
| `EVENT_ADD_PAYMENT_INFO`        | Payment info added during checkout             |
| `EVENT_ADD_TO_CART`             | Item added to cart                             |
| `EVENT_BUTTON_CLICK`            | Button clicked                                 |
| `EVENT_PURCHASE`                | Payment completed                              |
| `EVENT_CONTENT_VIEW`            | Page viewed                                    |
| `EVENT_DOWNLOAD`                | Clicked download link (opens external browser) |
| `EVENT_FORM_SUBMIT`             | Form submitted                                 |
| `EVENT_INITIATED_CHECKOUT`      | Checkout process started                       |
| `EVENT_CONTACT`                 | Contact/consultation initiated                 |
| `EVENT_PLACE_ORDER`             | Order placed                                   |
| `EVENT_SEARCH`                  | Search performed                               |
| `EVENT_COMPLETE_REGISTRATION`   | Registration completed                         |
| `EVENT_ADD_TO_WISHLIST`         | Item added to wishlist                         |
| `EVENT_SUBSCRIBE`               | Subscription completed                         |
| `EVENT_FIRST_DEPOSIT`           | First deposit made                             |
| `EVENT_CREDIT_APPROVAL`         | Credit approved                                |
| `EVENT_LOAN_APPLICATION`        | Loan application submitted                     |
| `EVENT_LOAN_CREDIT`             | Loan approved                                  |
| `EVENT_LOAN_DISBURSAL`          | Loan disbursed                                 |
| `EVENT_CREDIT_CARD_APPLICATION` | Credit card application submitted              |
| `EVENT_VALUE_PRODUCE`           | Value generated                                |
| `EVENT_KEY_INAPP_EVENT`         | Key in-app event                               |
| `EVENT_KEY_INAPP_EVENT_1`       | Key in-app event 1                             |
| `EVENT_KEY_INAPP_EVENT_2`       | Key in-app event 2                             |
| `EVENT_KEY_INAPP_EVENT_3`       | Key in-app event 3                             |
| `EVENT_AD_VIEW`                 | (In-page) ad viewed                            |
| `EVENT_AD_CLICK`                | (In-page) ad clicked                           |

### Event Attributes

Populate the `data` field with the following attributes:

| ​**Attribute**​    | ​**Description**​                                                                                                                                            | ​**Required/Optional**​ | ​**Value Type**​                    |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ----------------------- | ----------------------------------- |
| `content_id`       | Product/content identifier                                                                                                                                   | Optional                | string                              |
| `content_type`     | Must be `product` or `product_group`, based on product catalog configuration. Use `product` for single-item events, `product_group`for product group events. | Optional                | `product` or `product_group`        |
| `contents`         | Required for multiple content IDs. Must include sub-objects: `id`(product ID) and `quantity` (number of items added/purchased).                              | Optional                | Array of objects (`id`, `quantity`) |
| `content_category` | Page/product category                                                                                                                                        | Optional                | string                              |
| `content_name`     | Page/product name                                                                                                                                            | Optional                | string                              |
| `currency`         | Currency code (e.g., USD, BRL, IDN) per ISO 4217. Default: USD if empty.                                                                                     | Optional                | string (UPPERCASE)                  |
| `value`            | Total order value (e.g., 10.13). ​**Strongly recommended for paid events.**​​                                                                                | Optional                | number                              |
| `quantity`         | Number of items added to cart or purchased                                                                                                                   | Optional                | number                              |
| `price`            | Unit price (e.g., 4.99)                                                                                                                                      | Optional                | number                              |
| `query`            | Search query string (used with `EVENT_SEARCH`)                                                                                                               | Optional                | string                              |

### Multiple Items Example (e.g., Purchase/Cart)

```json
{
  "eid": "EVENT_PURCHASE",
  "pixel_click_id": "0_0_1t5lia_6Nx_2YH_6kW_0_5md7hw6Qi0m6p105dTsOyV",
  "data": {
    "value": 12998,
    "currency": "USD",
    "items": [
      {
        "content_id": "111111",
        "content_type": "phone",
        "content_name": "iPhone 15",
        "price": "5999",
        "quantity": 1,
        "currency": "USD"
      },
      {
        "content_id": "222222",
        "content_type": "phone",
        "content_name": "iPhone 15 Pro",
        "price": "6999",
        "quantity": 1,
        "currency": "USD"
      }
    ]
  },
  "ip": "106.215.139.186"
}
```
