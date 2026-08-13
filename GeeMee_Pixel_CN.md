# GeeMee Pixel

## 1. 什么是 Pixel

GeeMee Pixel 追踪标签是一段代码片段，可以帮助您衡量和了解网站上的用户行为，从而更轻松地追踪广告效果。它异步加载，不会影响您的网站加载速度或用户体验。

您可以使用 GeeMee Pixel 实现以下功能：

> *衡量广告效果：通过定义事件的广告效果，衡量广告投放的成效。

> *系统优化投放：通过设置优化目标，系统将根据优化目标自动调整投放策略，从而覆盖更多可能采取关键行动的用户，例如加入购物车、完成购买等。

## 2. 使用方法

### 1. 注册应用/网站

在开始之前，您需要在 GeeMee 平台注册您的网站：

1. 通过自助注册或商务开户获取 GeeMee 平台的账号密码
2. 进入 GeeMee 平台，在 App 页面注册应用/App，并根据页面引导完成网站注册

### 2. Pixel 基础代码

在 App 中注册成功后，您可以从页面获取网站的 Pixel ID，并将其替换到以下基础代码中：

```javascript
<!-- GeeMee 加载器文件 [必需] -->
    <script type="text/javascript" src="https://s.geemee.ai/js/tag.js?aa=## 请在此处输入您网站的 Pixel-ID ##">
    </script>
<!-- END GeeMee 加载器文件 -->
```

> Pixel 基础代码是启用 GeeMee 追踪后续标签事件的必要条件。请将以下脚本放置在网站所有页面的 `<head>` 标签中，确保它被包含在所有页面上。每个页面只需触发一次。如果在同一页面上多次调用该脚本，不会产生任何影响。

请注意，不要将 Pixel 基础代码放入 `iframe` 内。

## 3. Pixel 事件代码

> 在安装事件代码之前，请确保您已经安装了基础代码。如果没有基础代码，单独的事件代码将无法运行。

> GeeMee Pixel 不支持自定义事件。您必须使用下文中定义的事件名称。

### 3.1 Pixel 支持的事件

Pixel 支持采集的事件及其说明如下：

| **事件名称**                      | **说明**                        |
| ----------------------------- | ----------------------------- |
| EVENT_ADD_PAYMENT_INFO        | 在结算流程中添加付款信息时触发               |
| EVENT_ADD_TO_CART             | 将商品添加到购物车时触发 *该事件对应的优化目标为「加购」 |
| EVENT_BUTTON_CLICK            | 点击按钮时触发                       |
| EVENT_PURCHASE                | 完成付款时触发 *该事件对应的优化目标为「付费」      |
| EVENT_CONTENT_VIEW            | 浏览页面时触发 *该事件对应的优化目标为「浏览内容」    |
| EVENT_DOWNLOAD                | 点击「打开外部浏览器下载页面」按钮时触发          |
| EVENT_FORM_SUBMIT             | 提交表单时触发                       |
| EVENT_INITIATED_CHECKOUT      | 开始结算流程时触发                     |
| EVENT_CONTACT                 | 联系或咨询时触发                      |
| EVENT_PLACE_ORDER             | 下订单时触发                        |
| EVENT_SEARCH                  | 执行搜索时触发                       |
| EVENT_COMPLETE_REGISTRATION   | 完成注册时触发 *该事件对应的优化目标为「注册」      |
| EVENT_ADD_TO_WISHLIST         | 将商品添加到心愿单时触发                  |
| EVENT_SUBSCRIBE               | 完成订阅时触发                       |
| EVENT_FIRST_DEPOSIT           | 首次充值/存款时触发                    |
| EVENT_CREDIT_APPROVAL         | 授信审批通过时触发                     |
| EVENT_LOAN_APPLICATION        | 贷款申请时触发                       |
| EVENT_LOAN_CREDIT             | 贷款审批通过时触发                     |
| EVENT_LOAN_DISBURSAL          | 贷款放款时触发                       |
| EVENT_CREDIT_CARD_APPLICATION | 信用卡申请时触发                      |
| EVENT_KEY_INAPP_EVENT         | 关键事件触发                        |
| EVENT_KEY_INAPP_EVENT_1       | 关键事件 1 触发                     |
| EVENT_KEY_INAPP_EVENT_2       | 关键事件 2 触发                     |
| EVENT_KEY_INAPP_EVENT_3       | 关键事件 3 触发                     |
| EVENT_AD_VIEW                 | 广告浏览时触发（网站端）                  |
| EVENT_AD_CLICK                | 广告点击时触发                       |
| EVENT_PWA_INSTALL             | 用户发起PWA应用安装                   |
| EVENT_PWA_OPEN                | 用户安装PWA应用后，尝试唤起PWA应用          |
| EVENT_PWA_ACTIVATE            | 用户安装PWA应用后，首次打开PWA应用          |
| EVENT_LOGIN                   | 用户登录                          |

### 3.2 Pixel 采集的事件属性

| **属性**           | **说明**                                                                                                                                           | **是否必填**            | **类型**                                      |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------- | ------------------------------------------- |
| content_id       | 商品或内容的标识符                                                                                                                                        | 可选                  | string                                      |
| content_type     | content_type 对象的属性值必须设置为 `product` 或 `product_group`，具体取决于设置商品目录时数据源的配置。如果您希望监测与单个商品相关的事件，请将值设置为 `product`。如果您希望监测与商品组相关的事件，请设置为 `product_group` | 可选                  | json                                        |
| contents         | 当有多个 content_id 时，请使用 `contents`。如果在参数中使用 `contents`，则子对象中必须包含以下内容：商品 ID（id）和数量（quantity，即加入购物车或购买的商品数量）                                         | 可选                  | 必须为对象数组（content 参数中包含 id 子对象和 quantity 子对象） |
| content_category | 页面/商品的类别                                                                                                                                         | 可选                  | string                                      |
| content_name     | 页面/商品的名称                                                                                                                                         | 可选                  | string                                      |
| currency         | 指社会经济活动中用作流通手段的货币，如美元。根据 [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) 标准，值应使用大写英文字母，如 "USD"、"BRL"、"IDR"                                    | 可选，如果留空则默认视为 USD    | 枚举（字符串）                                     |
| value            | 订单总价，例如 10.13                                                                                                                                    | 可选。强烈建议付费事件优化时包含此字段 | number                                      |
| quantity         | 用户添加到购物车或购买的商品数量                                                                                                                                 | 可选                  | number                                      |
| price            | 商品单价，例如 4.99                                                                                                                                     | 可选                  | number                                      |
| query            | 与搜索事件配合使用。用户输入的搜索字符串                                                                                                                             | 可选                  | string                                      |

> 注意："price" 是单个商品的价格，"value" 是订单的总价。例如，如果用户订购了两件商品，每件售价 $10，则 "price" 参数传 "10"，"value" 参数传 "20"。

> 当前支持的货币：巴西雷亚尔（BRL）、印尼卢比（IDR）和美元（USD）。

### 3.3 安装 Pixel 事件代码

当您的用户触发某些事件时，需要调用以下代码：

```javascript
<!-- 上报事件 -->
    <script type="text/javascript">
        window._atTag = window._adTag || []
        window._atTag.push({
            "eid":"## 在此处输入事件名称 ##",
            "data":{}
        })
    </script>
    <!-- END 上报事件 -->
```

例如，如果您需要监测的事件是用户购买，则需要将 eid 中的内容替换为 "EVENT_PURCHASE"：

```javascript
<!-- 上报事件 -->
    <script type="text/javascript">
        window._atTag = window._adTag || []
        window._atTag.push({
            "eid":"EVENT_PURCHASE",
            "data":{}
        })
    </script>
    <!-- END 上报事件 -->
```

### 3.4 为事件代码添加事件参数

为了更好地优化深度事件、降低投放成本并提升投放效果，我们建议您在事件监测中添加用户事件参数。

例如，用户订阅了一个 App 会员，单价为 $9.9，可携带以下参数：

```javascript
<!-- 上报事件 -->
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
    <!-- END 上报事件 -->
```

例如，用户在将商品加入购物车后提交了订单，可携带以下参数：

当有多个商品时，使用 "items" 数组分别列出：

```javascript
<!-- 上报事件 -->
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
                     "currency":"USD"
              ],
              [
                     "content_id":"222222",
                     "content_type":"vip",
                     "content_name":"iPhone 15 Pro",
                     "price":"9.9",
                     "quantity":1,
                     "value":"9.9",
                     "currency":"USD"
              ]
    }
        })
    </script>
    <!-- END 上报事件 -->
```

## 4. 确保事件正常上报（非常重要）

在广告投放过程中，GeeMee 会在落地页 URL 后添加用户参数，包括 Clickid、gaid、渠道标识等内容。如果您的链接包含重定向，请确保这些参数在实际展示给用户的页面路径中仍然存在。

例如：

1. 您的投放链接为：`https://www.geemee.ai`
2. 当用户通过广告点击进入页面时，链接将变为：
`https://www.geemee.ai?click_id=0_0_1siTAu_67l_1tj_6kW_4An0_1qvJW1VfQNxPyEmFNRWo6p&utm_source=geemee`
3. 如果您的投放链接包含重定向逻辑，需要确保参数在重定向到新页面后仍然存在：
`https://www.geemeexxxxxxxx.ai?click_id=0_0_1siTAu_67l_1tj_6kW_4An0_1qvJW1VfQNxPyEmFNRWo6p&utm_source=geemee`

完成以上步骤后，请联系我们的 BM 完成对接的人工验收，以确保可正常监测事件。

## 5. 常见问题

### 1. 标签代码会影响页面加载速度吗？

标签代码不会影响您的页面加载速度。它采用异步加载方式，不会影响网站的加载时间或用户体验。

### 2. `_adTag` 的作用是什么？

`_adTag` 是一个 window 级别的变量，用于临时存储事件相关数据。当事件发送完毕后，该变量将被清空。

### 3. 落地页的域名是 `a.com`，事件页的域名是 `b.com`，这会影响事件的采集吗？如果会，该如何处理？

这种情况下，您应该将加载器脚本放在 `b.com` 中。如果登录页包含参数，必须将这些参数传递到事件发生的页面上。
