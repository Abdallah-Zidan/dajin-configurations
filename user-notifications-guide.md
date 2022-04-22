## User

### Comment approved
    - type: CommentApprovedNotification
    - id: commentable_id ( the news or article that has the comment)
    - parent : 'news'  in case of news and 'article' in case of article

### On Demand Notification
    - type: OnDemandNotification  

---
## Trader

### Trader Order Past Due Notification
    - type: TraderOrderPastDueNotification
    - id : order request id

### Request Accepted by farmer Notification
    - type: RequestAcceptedNotification
    - id : order request id

### New Tawreed Order  Notification
    - type: NewTawreedOrderNotification
    - id : tawreed order id

### Account Activation Notification
    - type: AccountActivationNotification
---
## Farmer

### Farm Ready For Selling Soon
    - type: FarmReadyForSellingSoon
    - id : farm id

### New Order Request Notification
    - type: NewOrderRequestNotification
    - id: order request id

### Order Done By Trader Notification
    - type: OrderDoneByTraderNotification
    - id : order request id

### Farm Activation Notification
    - type: FarmActivationNotification
    - id : farm id

