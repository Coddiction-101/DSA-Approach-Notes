> 🔢 **Pattern: Array – Stock Problems**  
> Best time to buy and sell stock (I, II, III, with cooldown, with fee).

---

### ✅ 1. Best Time to Buy and Sell Stock I (One Transaction)

**Idea:**  
- Track minimum price so far.  
- At each day, compute profit if sold today: `price[i] - minPrice`.  
- Keep maximum profit.

```cpp
int maxProfit(vector<int>& prices) {
    if (prices.size() <= 1) return 0;
    
    int minPrice = prices;
    int maxProfit = 0;
    
    for (int i = 1; i < prices.size(); i++) {
        maxProfit = max(maxProfit, prices[i] - minPrice);
        minPrice = min(minPrice, prices[i]);
    }
    
    return maxProfit;
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 2. Best Time to Buy and Sell Stock II (Multiple Transactions)

**Idea:**  
- Buy on every local minimum, sell on every local maximum.  
- Or, simply add every positive price difference (greedy).

```cpp
int maxProfit(vector<int>& prices) {
    int profit = 0;
    for (int i = 1; i < prices.size(); i++) {
        if (prices[i] > prices[i-1]) {
            profit += prices[i] - prices[i-1];
        }
    }
    return profit;
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 3. Best Time to Buy and Sell Stock III (At Most Two Transactions)

**Idea:**  
- Use DP: `buy1`, `sell1`, `buy2`, `sell2`.  
- At each day, update the best state for each of these.

```cpp
int maxProfit(vector<int>& prices) {
    if (prices.size() <= 1) return 0;
    
    int buy1 = -prices, sell1 = 0;
    int buy2 = -prices, sell2 = 0;
    
    for (int i = 1; i < prices.size(); i++) {
        buy1  = max(buy1,  -prices[i]);           // first buy
        sell1 = max(sell1, buy1 + prices[i]);     // first sell
        buy2  = max(buy2,  sell1 - prices[i]);    // second buy
        sell2 = max(sell2, buy2 + prices[i]);     // second sell
    }
    
    return sell2;
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 4. Best Time to Buy and Sell Stock with Cooldown

**Idea:**  
- Maintain three states: `hold`, `sold`, `rest` (cooldown).  
- Transition between states.

```cpp
int maxProfit(vector<int>& prices) {
    if (prices.size() <= 1) return 0;
    
    int hold = -prices;  // holding a stock
    int sold = 0;           // just sold (in cooldown)
    int rest = 0;           // not holding, not in cooldown
    
    for (int i = 1; i < prices.size(); i++) {
        int prevHold = hold, prevSold = sold, prevRest = rest;
        
        hold = max(prevHold, prevRest - prices[i]);  // buy from rest
        sold = prevHold + prices[i];                 // sell from hold
        rest = max(prevRest, prevSold);              // stay in rest or come from sold
    }
    
    return max(sold, rest);
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ✅ 5. Best Time to Buy and Sell Stock with Transaction Fee

**Idea:**  
- Maintain two states: `hold` (owning stock), `cash` (no stock).  
- Subtract fee when selling.

```cpp
int maxProfit(vector<int>& prices, int fee) {
    int hold = -prices;  // holding a stock
    int cash = 0;           // no stock
    
    for (int i = 1; i < prices.size(); i++) {
        int prevHold = hold, prevCash = cash;
        
        hold = max(prevHold, prevCash - prices[i]);      // buy
        cash = max(prevCash, prevHold + prices[i] - fee); // sell with fee
    }
    
    return cash;
}
```

- **Time:** O(n)  
- **Space:** O(1)

---

### ⏱️ Complexity Summary

| Problem Type                     | Time       | Space     |
|----------------------------------|------------|-----------|
| Stock I (1 transaction)          | O(n)       | O(1)      |
| Stock II (unlimited transactions)| O(n)       | O(1)      |
| Stock III (2 transactions)       | O(n)       | O(1)      |
| Stock with Cooldown              | O(n)       | O(1)      |
| Stock with Fee                   | O(n)       | O(1)      |

---

### 📌 Key Takeaways

- **Stock I**: track `minPrice` and `maxProfit`.  
- **Stock II**: greedy — add every positive difference.  
- **Stock III**: use four variables (`buy1`, `sell1`, `buy2`, `sell2`).  
- **Cooldown**: use three states (`hold`, `sold`, `rest`).  
- **With Fee**: use two states (`hold`, `cash`) and subtract fee on sell.  
- Always handle edge cases: empty array, single day.
```
