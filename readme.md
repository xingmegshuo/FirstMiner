# 智蚂蚁量化交易

## 简述

量化交易计划任务，开启协程监听价格波动，在价格下跌时买入在价格上升时卖出以此达到盈利目的，目前以支持火币现货，币安现货

## 参数详解

> 1. 数量 num 买进次数
> 2. price 第一次买入时价格
> 3. price_rate 补仓比例 价格持续下跌买入多少
> 4. price_growth 补仓增幅 在上次买入的基础上追加
> 5. price_callback 回调 持续下跌过程到达涨幅买入
> 6. price_stop 止盈 赚钱到达一定比列平仓
> 7. price_reduce 回降 价格超过止盈还在上涨不用处理下降到达此比例时平仓

## 计算方式

- 第一单，进场速度快
- 之后进场时机价格持续下降不买入，到达回调比例买入  

### example

> 做单数量3，补仓比例20% 跌幅 0.5 补仓增幅 50 %

| 单数    | 价格                | 买入数量       | 跌幅        | 投入金额       |
| ------- | ------------------- | -------------- | ----------- | -------------- |
| 单数: 1 | 价格: 0.258513      | 买入数量:23.21 | 跌幅: 0.5   | 花费资金: 6    |
| 单数: 2 | 价格: 0.2565741525  | 买入数量:28.06 | 跌幅: 0.75  | 花费资金: 7.2  |
| 单数: 3 | 价格: 0.25366588125 | 买入数量:34.06 | 跌幅: 1.125 | 花费资金: 8.64 |

## 策略分类

### 智乘方 `限/市`

> 智乘方策略为整体出仓方式,在价格下降过程中持续买入，到达止盈比例和回降比例后卖出之前买入的全部, 限表示限价买入方式以指定价格成交, 市表示以市场最优价格成交

### 智多元 `限/市`

> 智多元为逐单平仓方式, 计算每一单买入的盈利, 当一单到达盈利后卖出这一单, 下次跌幅到此单比例继续买入，当所有单数卖出结束, 限和市与以上相同
