- [返回首页](https://github.com/DuHouAn/Java-Interview)

# 股票交易问题

## 121 
[121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

```html
> 问题描述：
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。
如果你**最多只允许完成一笔交易**（即买入和卖出一支股票），设计一个算法来计算你所能获取的最大利润。
注意你不能在买入股票前卖出股票。

> 示例：
示例 1:
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，
最大利润 = 6-1 = 5 。注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。

示例 2:
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

```java
//思路一:暴力解法，但是效率不高
// 如果想获利，则必须低价买入，然后高价卖出。
// 如果不能获利，则只能不进行交易。
// 时间复杂度：时间复杂度：O(n^2)
public int maxProfit(int[] prices) {
    int n = prices.length;
    if(n==0 || n==1){
        return 0;
    }
    int res  = 0 ;
    for(int i=0;i<n;i++){
        for(int j = n-1;j>i;j--){
            res = Math.max(prices[j]-prices[i],res);
        }
    }
    return res;
}
```

```java
//思路二:
//使用minStock用来维护数组中的最小值，maxProfit来维护最大收益
// 时间复杂度：时间复杂度：O(n)
public int maxProfit(int[] prices) {
    int n = prices.length;
    if(n==0 || n==1){
        return 0;
    }
    int minValue = prices[0];
    //初始时，不进行交易，当然收益为0
    int maxProfit  = 0 ;
    for(int i=1;i<n;i++){
        minValue = Math.min(minValue,prices[i]);
        maxProfit = Math.max(maxProfit,prices[i]-minValue);
    }
    return maxProfit;
}
```

## 122
[122. 买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

```html
> 问题描述：
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。
设计一个算法来计算你所能获取的最大利润。**你可以尽可能地完成更多的交易**（多次买卖一支股票）。
注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

> 示例：
示例 1:
输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出,  这笔交易所能获得利润 = 6-3 = 3 。

示例 2:
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。

示例 3:
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

```java
//思路：贪心策略，只要相邻两天中，股价上涨就买，尽量多的进行交易
public int maxProfit(int[] prices) {
    int n = prices.length;
    if(n==0 || n==1){
        return 0;
    }
    int maxProfit = 0;
    for(int i=1;i<n;i++){
        if(prices[i]>prices[i-1]){ //只要相邻两天中，股价上涨就进行交易
            maxProfit += prices[i] - prices[i-1];
        }
    }
    return maxProfit;
}
```
## 123
[123. 买卖股票的最佳时机 III](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/)

```html
> 问题描述：
给定一个数组，它的第 i 个元素是一支给定的股票在第 i 天的价格。
设计一个算法来计算你所能获取的最大利润。**你最多可以完成 两笔 交易**。
注意: 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

> 示例：
示例 1:
输入: [3,3,5,0,0,3,1,4]
输出: 6
解释: 在第 4 天（股票价格 = 0）的时候买入，在第 6 天（股票价格 = 3）的时候卖出，这笔交易所能获得利润 = 3-0 = 3 。
随后，在第 7 天（股票价格 = 1）的时候买入，在第 8 天 （股票价格 = 4）的时候卖出，这笔交易所能获得利润 = 4-1 = 3 。

示例 2:
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 
这笔交易所能获得利润 = 5-1 = 4 。   
注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。

示例 3:
输入: [7,6,4,3,1] 
输出: 0 
解释: 在这个情况下, 没有交易完成, 所以最大利润为 0。
```

```java
//思路：
//对于任意一天考虑四个变量:
//buy1: 在当天第一次买入股票可获得的最大收益
//sell1: 在当天第一次卖出股票可获得的最大收益
//buy2: 在当天第二次买入股票可获得的最大收益
//sell2: 在当天第二次卖出股票可获得的最大收益
//分别对四个变量进行相应的更新, 最后sell2就是最大
public int maxProfit(int[] prices) {
    int n = prices.length;
    if(n==0 || n==1){
        return 0;
    }

    //在当天第一次买入股票可获得的最大收益
    int buy1 = Integer.MIN_VALUE;
    //在当天第一次卖出股票可获得的最大收益
    int sell1 = 0 ;
    //在当天第二次买入股票可获得的最大收益
    int buy2 = Integer.MIN_VALUE;
    //在当天第二次卖出股票可获得的最大收益
    int sell2 = 0 ;
    for(int price : prices){
        buy1 = Math.max(buy1,-price); // 当天买入股票损失price
        sell1 = Math.max(sell1,buy1+price); //当天卖出股票后可得 price
        buy2 = Math.max(buy2,sell1-price);
        sell2 = Math.max(sell2,buy2+price);
    }
    return sell2;
}
```

## 188
[188. 买卖股票的最佳时机 IV](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iv/)

```html
> 问题描述：

给定一个数组，它的第 i 个元素是一支给定的股票在第 i 天的价格。
设计一个算法来计算你所能获取的最大利润。**你最多可以完成 k 笔交易**。
注意: 你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

> 示例：
示例 1:
输入: [2,4,1], k = 2
输出: 2
解释: 在第 1 天 (股票价格 = 2) 的时候买入，在第 2 天 (股票价格 = 4) 的时候卖出，这笔交易所能获得利润 = 4-2 = 2 。

示例 2:
输入: [3,2,6,5,0,3], k = 2
输出: 7
解释: 在第 2 天 (股票价格 = 2) 的时候买入，在第 3 天 (股票价格 = 6) 的时候卖出, 这笔交易所能获得利润 = 6-2 = 4 。
随后，在第 5 天 (股票价格 = 0) 的时候买入，在第 6 天 (股票价格 = 3) 的时候卖出, 这笔交易所能获得利润 = 3-0 = 3 。
```

```java
//思路：
//1、因为需要先买入，然后再卖出，则在n天最多只能进行 n/2次交易。k>=n/2时，此时问题就转化为 122 题中的尽可能多的完成交易。
//2、对于其他的k, 在123中定义了2组买入和卖出时最大收益的变量, 在这里就使用k组这样的变量,
// 这样问题IV是对问题III的推广, profit[i][0]表示第i比交易买入的最大收益，profit[i][1]表示第i比交易卖出时的最大收益
public int maxProfit(int k, int[] prices) {
    if(k<=0){ //TODO:k==0，说明不能交易，此时收益为0
        return 0;
    }
    int n = prices.length;
    if(n == 0 || n==1){
        return 0;
    }
    int maxProfit = 0;
    if(k>=n/2){
       return maxProfit2(prices);
    }

    int[][] profit = new int[k+1][2];
    for(int i=1;i<k+1;i++){
        profit[i][0] = Integer.MIN_VALUE;
        profit[i][1] = 0;
    }

    for(int price : prices){
        //第1次交易
        profit[1][0] = Math.max(profit[1][0],-price);
        profit[1][1] = Math.max(profit[1][1],profit[1][0]+price);
        for(int i=2;i<=k;i++){
            //接下来进行(k-1)次交易
            profit[i][0] = Math.max(profit[i][0],profit[i-1][1] - price);
            profit[i][1] = Math.max(profit[i][1],profit[i][0]+price);
        }
    }
    return profit[k][1];
}

private int maxProfit2(int[] prices){
    int n = prices.length;
    if(n<=1){
        return 0;
    }
    int maxProfit = 0;
    for(int i=1;i<n;i++){
        if(prices[i]>prices[i-1]){
            maxProfit += prices[i]-prices[i-1];
        }
    }
    return maxProfit;
}
```

## 309
[309. 最佳买卖股票时机含冷冻期](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/)

```html
> 问题描述：
给定一个整数数组，其中第 i 个元素代表了第 i 天的股票价格 。​
设计一个算法计算出最大利润。在满足以下约束条件下，你可以**尽可能地完成更多的交易**（多次买卖一支股票）:
你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。
卖出股票后，你无法在第二天买入股票 (即冷冻期为 1 天)。

> 示例:

输入: [1,2,3,0,2]
输出: 3 
解释: 对应的交易状态为: [买入, 卖出, 冷冻期, 买入, 卖出]
```

```java
//思路：
//1、总共有三个状态：持有股票，卖掉股票，冷却一天，后两种都可以归纳为未持有股票。我们这里就讨论持有股票和未持有股票的状态。
//2、今天未持有股票的状态,最大利润有两种可能：
//(1)和昨天一样保持未持有状态,维持昨天的状态；
//(2)将昨天持有股票今天卖掉；
//notHold[i] = max{notHold[i-1],hold[i-1]+prices[i]};
//3、今天持有股票的状态，最大利润有两种可能：
//(1)和昨天一样持有股票不卖。
//(2)两天前(因为未持有就是卖出了，第二天不能买入，要想买入必须再过一天)未持有,今天才能购买。
// hold[i] = max{hold[i-1],notHold[i-2]-price[i]};
public int maxProfit(int[] prices) {
   int n = prices.length;
   if(n<=1){
       return 0;
   }

   int[] notHold = new int[n];
   int[] hold = new int[n];

   notHold[0] = 0;//第1天不可能进行交易，初始化最大收益为0
    hold[0] = -prices[0]; //第一天持有股票，只能买入

    for(int i=1;i<prices.length;i++){
        notHold[i] = Math.max(notHold[i-1],hold[i-1]+prices[i]);
        hold[i] = (i>2)?
                Math.max(hold[i-1],notHold[i-2]-prices[i]) :  Math.max(hold[i-1],0-prices[i]);
    }
    return notHold[n-1];
}
```

## 714
[714. 买卖股票的最佳时机含手续费](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)

```html
> 问题描述：
给定一个整数数组 prices，其中第 i 个元素代表了第 i 天的股票价格 ；
非负整数 fee 代表了交易股票的手续费用。
你可以**无限次地完成交易**，但是你每次交易都需要付手续费。
如果你已经购买了一个股票，在卖出它之前你就不能再继续购买股票了。
返回获得利润的最大值。

> 示例：
示例 1:
输入: prices = [1, 3, 2, 8, 4, 9], fee = 2
输出: 8
解释: 能够达到的最大利润:  
在此处买入 prices[0] = 1
在此处卖出 prices[3] = 8
在此处买入 prices[4] = 4
在此处卖出 prices[5] = 9
总利润: ((8 - 1) - 2) + ((9 - 4) - 2) = 8.

> 注意:
0 < prices.length <= 50000.
0 < prices[i] < 50000.
0 <= fee < 50000.
```

```java
//思路：参考 309 题
//1、注意这里不需要休息1天了
//2、我们这里就讨论持有股票和未持有股票的状态。
//3、今天未持有股票的状态,最大利润有两种可能：
//(1)和昨天一样保持未持有状态,维持昨天的状态；
//(2)将昨天持有股票今天卖掉； (注意:手续费在卖出股票后再交)
//notHold[i] = max{notHold[i-1],hold[i-1]+prices[i]-fee};
//4、今天持有股票的状态，最大利润有两种可能：
//(1)和昨天一样持有股票不卖。
//(2)昨天未持有,今天购买。
// hold[i] = max{hold[i-1],notHold[i-1]-price[i]};
public int maxProfit(int[] prices, int fee) {
    int n = prices.length;
    if(n<=1){
        return 0;
    }

    //未持有股票，就是卖出
    int[] notHold = new int[n];
    int[] hold = new int[n];

    notHold[0] = 0;//第1天不可能进行交易，初始化最大收益为0
    hold[0] = -prices[0]; //第一天持有股票，只能买入

    for(int i=1;i<prices.length;i++){
        notHold[i] = Math.max(notHold[i-1],hold[i-1]+prices[i]-fee);
        hold[i] = Math.max(hold[i-1],notHold[i-1]-prices[i]);
    }
    return notHold[n-1];
}
```