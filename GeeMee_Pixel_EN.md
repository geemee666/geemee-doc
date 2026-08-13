# GeeMee Pixel_en

## 1. What is Pixel

The GeeMee Pixel tracking tag is a code snippet that can help you measure and understand user behavior on your website, making it easier to track ad effectiveness. It loads asynchronously and does not affect your website loading time or user experience.

You can use GeeMee Pixel to achieve the following functions:

> *Measuring advertising effectiveness: Measuring the effectiveness of advertising placement by defining the advertising effectiveness of events.

> *System optimization delivery: By setting optimization goals, the system will automatically adjust delivery according to the optimization goals, so as to cover more users who may take key actions, such as adding shopping carts, completing purchases, etc.

2.  Usage method

### 1.  Register an application/website

Before starting, you need to register your website on the GeeMee platform

1. Obtain GeeMeen platform account password through self-service registration or business account opening
2. Enter the GeeMe platform, register the application/app on the App page, and complete the website registration through the page guide

### 2. Pixel Basic Code

After successfully registering on the app, you can obtain the website's Pixel ID from the page and replace it in the basic code below

```javascript
<!-- GeeMee Loader File [Required] -->
    <script type="text/javascript" src="https://s.geemee.ai/js/tag.js?aa=## Please enter your website's Pixel-ID here ##">
    </script>
<!-- END GeeMee Loader File -->
```

> 

> The Pixel base code is required to enable GeeMee to trace the rest of the label events. Place the following script in the "head" included on all pages of your website, so that it will be included on all pages. It only needs to be triggered once on each page. If the script is called multiple times on a page, it will not have any impact.

Please note that do not put the Pixel basic code into the `iframe`.

3. Pixel event code

> Before installing event codes, make sure you have the base code. If there is no base code, the separate event code cannot run.

> GeeMee Pixel does not support custom events. You must use the event name defined below.

#### 3.1 Pixel supported events

Pixel supports collecting events and their descriptions are as follows:

| Event Name                    | Desc                                                                                                               |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| EVENT_ADD_PAYMENT_INFO        | When payment information is added to the settlement process                                                        |
| EVENT_ADD_TO_CART             | When an item is added to the cart* The corresponding optimization objective of this event is "additional purchase" |
| EVENT_BUTTON_CLICK            | When you click the button                                                                                          |
| EVENT_PURCHASE                | When payment is completed* The corresponding optimization goal of this event is "pay"                              |
| EVENT_CONTENT_VIEW            | When the page is viewed* The corresponding optimization goal of this event is "View Content"                       |
| EVENT_DOWNLOAD                | When you click the Open External Browser Download Page button                                                      |
| EVENT_FORM_SUBMIT             | When the form is submitted                                                                                         |
| EVENT_INITIATED_CHECKOUT      | When the closing process starts                                                                                    |
| EVENT_CONTACT                 | In case of contact or consultation                                                                                 |
| EVENT_PLACE_ORDER             | When an order is placed                                                                                            |
| EVENT_SEARCH                  | When a search occurs                                                                                               |
| EVENT_COMPLETE_REGISTRATION   | When registration is complete* The corresponding optimization target of this event is "Register"                   |
| EVENT_ADD_TO_WISHLIST         | When an item is added to the wish list                                                                             |
| EVENT_SUBSCRIBE               | When the subscription is complete                                                                                  |
| EVENT_FIRST_DEPOSIT           | First deposit                                                                                                      |
| EVENT_CREDIT_APPROVAL         | Credit                                                                                                             |
| EVENT_LOAN_APPLICATION        | Loan application                                                                                                   |
| EVENT_LOAN_CREDIT             | Loan approval                                                                                                      |
| EVENT_LOAN_DISBURSAL          | Loan disbursement                                                                                                  |
| EVENT_CREDIT_CARD_APPLICATION | Credit card application                                                                                            |
| EVENT_KEY_INAPP_EVENT         | Key events                                                                                                         |
| EVENT_KEY_INAPP_EVENT_1       | Key Event 1                                                                                                        |
| EVENT_KEY_INAPP_EVENT_2       | Key Event 2                                                                                                        |
| EVENT_KEY_INAPP_EVENT_3       | Key Event 3                                                                                                        |
| EVENT_AD_VIEW                 | (On the website) Advertising viewing                                                                               |
| EVENT_AD_CLICK                | Ad click                                                                                                           |
| EVENT_PWA_INSTALL             | User initiates PWA application installation                                                                        |
| EVENT_PWA_OPEN                | After the user installs the PWA application, try to invoke the PWA application                                     |
| EVENT_PWA_ACTIVATE            | After the user installs the PWA application, opening the PWA application for the first time                        |
| EVENT_LOGIN                   | User Login                                                                                                         |

#### 3.2 Event attributes collected by Pixel

| Optional         | **Desc**                                                                                                                                                                                                                                                                                                                                                                            | **Required**                                                                   | **Type**                                                                            |
| ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------- |
| content_id       | Identifier of product or content                                                                                                                                                                                                                                                                                                                                                    | Optional                                                                       | string                                                                              |
| content_type     | The attribute value of the content_type object must be set to product or product_group, depending on the configuration of the data feed when setting the product directory. If you want to monitor events related to a single product, set the value to product. If you want to monitor events related to a product group, set it to product_group                                  |                                                                                | json                                                                                |
| contents         | When there are multiple content IDs, please use contents. If contents is used in the parameter, the following contents must be included in the sub object: product ID, and quantity (quantity of items added to the shopping cart or purchased)                                                                                                                                     |                                                                                | Must be an object array (content parameter, id sub object and quantity sub object). |
| content_category | Category of page/product                                                                                                                                                                                                                                                                                                                                                            | Optional                                                                       | string                                                                              |
| content_name     | Name of page/product                                                                                                                                                                                                                                                                                                                                                                | Optional                                                                       | string                                                                              |
| currency         | Refers to the currency used as a means of circulation in social and economic activities, such as the US dollar. According to[ [https://en.wikipedia.org/wiki/ISO_4217](https://en.wikipedia.org/wiki/ISO_4217) ]（ [https://en.wikipedia.org/wiki/ISO_4217](https://en.wikipedia.org/wiki/ISO_4217) ）, the value should be in uppercase English letters, such as "USD", "BRL", "IDN" | Optional, if it is blank, it will be deemed as USD                             | Enumeration (string)                                                                |
| value            | Total order price, e.g. 10.13                                                                                                                                                                                                                                                                                                                                                       | Optional. Customers strongly recommend that payment event optimization include | number                                                                              |
| quantity         | Number of products added to shopping cart or purchased by users                                                                                                                                                                                                                                                                                                                     | Optional                                                                       | number                                                                              |
| price            | Commodity price, in yuan, for example, 4.99                                                                                                                                                                                                                                                                                                                                         | Optional                                                                       | number                                                                              |
| query            | Used with search events. The search string entered by the user                                                                                                                                                                                                                                                                                                                      | Optional                                                                       | string                                                                              |

> Note: "price" is the price of a single commodity, and "value" is the total price of the order. For example, if the user orders two goods, each of which sells for $10, the "price" parameter will pass "10" and the "value" parameter will pass "20".

> Currently supported currencies: Brazilian Riyal (BRL), Indonesian Rupiah (IDR) and United States Dollar (USD).

#### 3.3 Installing Pixel Event Codes

When your user triggers some events, you need to call the following code

For example, if the event you need to monitor is purchased by the user, you need to replace the content in eid with "EVENT_PURCHASE":

```javascript
    <!-- Report Event -->
    <script type="text/javascript">
        window._atTag = window._adTag || []
        window._atTag.push({
            "eid":"EVENT_PURCHASE",
            "data":{}
        })
    </script>
    <!-- END Report Event -->
```

#### 3.4 Adding Event Parameters to Event Codes

In order to better optimize in-depth events, reduce launch costs and improve launch effects, we recommend that you add user event parameters to event monitoring

For example, if a user subscribes to an App member and the unit price is $9.9, the following parameters can be carried:

```javascript
    <!-- Report Event -->
    <script type="text/javascript">
        window._adTag = window._adTag || []
        window._adTag.push({
            "eid":"EVENT_PURCHASE",
            "data":{
                "content_id":"111111",
                "content_type":"vip",
                "content_name":"Vip subscription",
                "value":"9.9",
                "currency":"USD",
                "price":""
    }
        })
    </script>
    <!-- END Report Event -->
```

For example, when a user submits an order after adding goods to a shopping cart, the following parameters can be carried:

When there are multiple items, use "items" to list them separately

```javascript
    <!-- Report Event -->
    <script type="text/javascript">
        window._adTag = window._adTag || []
        window._adTag.push({
            "eid":"EVENT_PURCHASE",
            "data":{
                "items":[
                     "content_id":"111111",
                     "content_type":"vip",
                     "content_name":"iPhone 15",
                     "price":"9.9",
                     "quantity":1,
                     "value":"9.9",
                     "currency":"USD",
              ],
              [
                     "content_id":"222222",
                     "content_type":"vip",
                     "content_name":"iPhone 15 Pro",
                     "price":"9.9",
                     "quantity":1,
                     "value":"9.9",
                     "currency":"USD",
              ]
    }
        })
    </script>
    <!-- END Report Event -->
```

### 4.Ensure the normal reporting of events (very important)

During the advertising process, GeeMee will add user parameters after the landing page, including Clickid, gaid, channel identifier and other content. If your link contains redirection, please ensure that these parameters are included in the page path that is actually displayed to users.

For example:

1. Your launch link is: [https://www.geemee.ai](a)
2. When the user clicks through the advertisement to enter the page, the link will become:  [https://www.geemee.ai?click_id=0_0_1siTAu_67l_1tj_6kW_4An0_1qvJW1VfQNxPyEmFNRWo6p&utm_source=geemee](a)
3. If your launch link contains redirection logic, you need to ensure that the parameters still exist after redirecting to the new page: [https://www.geemeexxxxxxxx.ai?click_id=0_0_1siTAu_67l_1tj_6kW_4An0_1qvJW1VfQNxPyEmFNRWo6p&utm_source=geemee](b)

After completing the above steps, please contact our BM to complete the manual acceptance of the docking time to ensure the events that can be monitored.

## 3. Frequently asked questions

### 1.Does the tag code affect the loading speed of the page?

The tag code will not affect your page loading speed. It is loaded asynchronously and will not affect your website's loading time or user experience.

### 2.What is the role of  `_adTag `?

` _adTag `is a window level variable used to temporarily store event related data. When the event is sent, the variable will be cleared.

### 3.The domain name of the landing page is`a.com`and the domain name of the event is`b.com`. Will this affect the collection of events? If so, how to deal with it?

In this case, you should put the loader script in `b.com`. If the login page has the parameter, the parameter must be passed to the page where the event occurs.
