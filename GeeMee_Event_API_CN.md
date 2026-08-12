# GeeMee Event API

Event Api为投放网页类广告的广告主提供了一个服务器与服务器之间的一个安全接口，通过向GeeMee平台（后续称“我方”）提供的接口发送转化事件，将用户在广告主网站上触发的事件直接共享给我方，让我方充分掌握信息，洞察网站访客的行为历程，从而更好地进行优化广告投放效果。

## 1.Event Api优势

1. 区别于Pixel，Event Api无需在页面中插入代码，仅需构建有效负载，并将有效负载发送至我方提供的接口即可
2. 区别于Pixel，Event Api支持跨域追踪
- 当用户的行为路径中包含除客户自己的域名之外的其他域名时，pixel无法完成事件上报，可使用Event Api进行事件上报
- 以巴西主流的boleto支付方式为例，boleto支付逻辑为，线上生成条形码，线下完成支付，此类场景无法使用Pixel进行支付事件追踪，可使用Event Api进行付费事件的回传
4. 区别于Pixel，Event Api支持多页面应用的网页的事件上报

## 2.Event Api的使用

### 请求地址

 [https://s.geemee.ai/e/s2s](https://s.geemee.ai/e/s2s)

> 注意，请使用Server发起回调并记录回调日志，且仅支持`POST`请求。

### 白名单配置

**在上线前，请将您的Server IP提供给 GeeMee ，白名单外的IP发起的回调将被拒绝。**

Header

Content-Type: application/json

### 请求参数

| **参数**         | **必选** | **类型** | **说明**                                                                                                                      |
| -------------- | ------ | ------ | --------------------------------------------------------------------------------------------------------------------------- |
| eid            | Y      | string | 事件名                                                                                                                         |
| pixel_click_id | Y      | string | 参数回传；click_id是跟踪参数，当广告投放用户点击广告并登陆您的网站时，将会创建一个唯一的 click_id并将其附加到 URL。此时，广告主应获取在广告投放链接中的“pixel_click_id”参数，并在用户发生转化时将参数回传给我方。 |
| pixel_id       | 是      | string | 我方平台分配给当前网站/ App的唯一ID                                                                                                       |
| data           | Y      | json   | 事件相关属性                                                                                                                      |
| ip             | Y      | string | 用户IP                                                                                                                        |

### 请求示例

```json
{
  "eid": "EVENT_CONTENT_VIEW",
  "pixel_click_id": "0_0_1t5lia_6Nx_2YH_6kW_0_5md7hw6Qi0m6p105dTsOyV",
  "pixel_id": "12345",
  "data": {
    "content_id": "111111",
    "content_type": "vip",
    "content_name": "会员订阅",
    "value": "9.9",
    "currency": "USD",
    "price": "1"
  },
  "ip": "106.215.139.186"
}

```

### 状态码

当Http请求状态为200，视作接口调用成功。

## 3.网页事件及属性

### 网页事件

请使用我方定义的标准事件，这有助于投放的优化。在下方事件列表中找到与用户行为最匹配的时间名称进行回传：

| 事件名称                          | 描述                   |
| ----------------------------- | -------------------- |
| EVENT_ADD_PAYMENT_INFO        | 当付款信息被添加到结账流程中。      |
| EVENT_ADD_TO_CART             | 当物品被添加至购物车。          |
| EVENT_BUTTON_CLICK            | 当点击按钮。               |
| EVENT_PURCHASE                | 当完成付款。               |
| EVENT_FIRST_DAY_PURCHASE      | 当用户首日首次入金/充值/购买      |
| EVENT_FTD                     | 当用户完成首次充值/入金/购买      |
| EVENT_REPEAT_PURCHASE         | 当用户完成重复充值/入金/购买      |
| EVENT_CONTENT_VIEW            | 当页面被查看。              |
| EVENT_DOWNLOAD                | 当点击打开外部浏览器下载页面按钮。    |
| EVENT_FORM_SUBMIT             | 当表格被提交。              |
| EVENT_INITIATED_CHECKOUT      | 当结账流程开始。             |
| EVENT_CONTACT                 | 当发生联络或咨询。            |
| EVENT_PLACE_ORDER             | 当订单下单。               |
| EVENT_SEARCH                  | 当发生搜索。               |
| EVENT_COMPLETE_REGISTRATION   | 当注册完成。               |
| EVENT_ADD_TO_WISHLIST         | 当物品被添加至心愿列表。         |
| EVENT_SUBSCRIBE               | 当订阅完成。               |
| EVENT_FIRST_DEPOSIT           | 首次入金                 |
| EVENT_FIRST_DAY_PURCHASE      | 首日首次入金/充值/购买         |
| EVENT_CREDIT_APPROVAL         | 授信                   |
| EVENT_LOAN_APPLICATION        | 贷款申请                 |
| EVENT_LOAN_CREDIT             | 贷款批准                 |
| EVENT_LOAN_DISBURSAL          | 贷款放款                 |
| EVENT_CREDIT_CARD_APPLICATION | 信用卡申请                |
| EVENT_VALUE_PRODUCE           | 价值产生                 |
| EVENT_KEY_INAPP_EVENT         | 关键事件                 |
| EVENT_KEY_INAPP_EVENT_1       | 关键事件1                |
| EVENT_KEY_INAPP_EVENT_2       | 关键事件2                |
| EVENT_KEY_INAPP_EVENT_3       | 关键事件3                |
| EVENT_AD_VIEW                 | （网页内）广告观看            |
| EVENT_AD_CLICK                | （网页内）广告点击            |
| EVENT_PWA_INSTALL             | 用户发起PWA应用安装          |
| EVENT_PWA_OPEN                | 用户安装PWA应用后，尝试唤起PWA应用 |
| EVENT_PWA_ACTIVATE            | 用户安装PWA应用后，首次打开PWA应用 |
| EVENT_LOGIN                   | 用户登录                 |

### 事件属性

Data字段中的内容，应使用以下内容填充

| **参数名**          | **描述**                                                                                                                                         | **必选或可选**         | **值类型**                    |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- | -------------------------- |
| content_id       | 产品或内容的标识符                                                                                                                                      | 可选                | 字符串                        |
| content_type     | content_type对象属性值须设为product或product_group，具体取决于设置产品目录时对数据feed进行的配置。如果要监测与单个产品相关的事件，请将值设置为product。如果要监测与产品组相关的事件，请将其设置为product_group。           | 可选                | 必须是product或product_group。  |
| contents         | 当有多个内容ID时，请使用contents。如果在参数中使用contents，则必须在子对象中包括以下内容：产品ID，以及数量（添加到购物车或购买的物品数量）。                                                               | 可选                | 必须是对象数组（内容参数、id子对象和数量子对象）。 |
| content_category | 页面/产品的类别                                                                                                                                       | 可选                | 字符串                        |
| content_name     | 页面/产品的名称                                                                                                                                       | 可选                | 字符串                        |
| currency         | 指在社会和经济活动中作为流通手段使用的货币，例如美元。根据[https://en.wikipedia.org/wiki/ISO_4217](https://en.wikipedia.org/wiki/ISO_4217)，该值应为大写英文字母表示，例如“USD”、“BRL”、“IDN” | 可选，若为空则认为美元(USA)  | 枚举（字符串）                    |
| value            | 订单总价，例如10.13                                                                                                                                   | 可选，付费事件优化客户强烈建议包括 | 数字                         |
| quantity         | 用户添加到购物车或购买的产品数量                                                                                                                               | 可选                | 数字                         |
| price            | 商品价格，单位为元，例如4.99                                                                                                                               | 可选                | 数字                         |
| query            | 与搜索事件一起使用。用户输入的搜索字符串。                                                                                                                          | 可选                | 字符串                        |

当存在多个内容时，比如电商网站的加购或下单时存在多个商品，应使用”item”汇总多个内容，示例：

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



