# 验证节点监控

## 功能点
### 监控验证者是否在验证人租中
> 每隔一段时间（暂时设置为10m，可以根据配置配件的`interval`字段来修改）主动访问指定节点的`/validators`服务来获取当前验证人组，然后查看配置的验证人地址是否在获取的验证人组中。如果没有在，则发送短信和邮件通知管理员。短信服务可以通过设置`enable`字段来控制开关。

> 如果监控的地址一直不在验证人集合中，发告警通知的时间间隔会按照倍数递增。例如：10秒，20秒，40秒，80秒，160秒，320秒，640秒，1280秒。。。

* 不足之处：

> * 指定节点数据没有同步到最新。
> * 指定节点作恶。

* 注意：

> * 是否有需求同时监控多个验证地址？

### 监控提议并自动投票
> 订阅`voting-period-start`事件，收到此事件时发送邮件通知管理员，如果`gov::autovote`字段设置为true时，会自动投票。把手工投票和自动投票结合起来以达到更好的治理效果,在收到订阅的`voting-period-start`事件后会开启一个goroutine检查投票情况，当过了设定的时间后还是没有投票的话，会自动投票，并把投票结果发送给管理员。可以在配置文件中配置自动投票的类型。

### 提供网页用于手工投票
> 暂时不用

## 部署
* 根据助记词恢复验证者账户到本地数据库

> `gaiacli keys add <name> --recover`

* 启动客户端的rest服务

> `gaiacli rest-server --chain-id=`

* 生成配置文件并进行设置

> `cp conf/app.conf.sample conf/app.conf`





