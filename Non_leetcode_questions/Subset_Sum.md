# Subset Sum
**Recursive Way (Gets TLE'd)**
```
def subsetSumToK(n, target, arr):
    
    def find(cur_sum, i):        
        
        if cur_sum == 0: return True
        
        if i == 0: return cur_sum == arr[0]
        
        take = False
        if cur_sum >= arr[i]: take = find(cur_sum - arr[i], i - 1)
        
        not_take = find(cur_sum, i - 1)
        
        return take or not_take
    
    return find(target, n - 1)
```
**TC: O(3^(N))
SC: O(N) for recursive stack**

**Memoization (Using Hashmap)**
```
def subsetSumToK(n, target, arr):
    
    dp = {}   
    def find(cur_sum, i):        
        
        if cur_sum == 0: return True
        
        if i == 0: return cur_sum == arr[0]
    
        if (cur_sum,i) in dp: return dp[(cur_sum,i)]
    
        take = False
        if cur_sum >= arr[i]: take = find(cur_sum - arr[i], i - 1)
        
        not_take = find(cur_sum, i - 1)
        
        dp[(cur_sum,i)] = take or not_take
        return dp[(cur_sum,i)]
    
    return find(target, n - 1)
```    
**TC: O(MxN)
SC: O(M+N) + O(MxN) for recursive stack and dp hashmap**

**Memoization (Using 2D array)**
```
def subsetSumToK(n, target, arr):
    
    dp = [[-1]*n for _ in range(target + 1)]
    def find(cur_sum, i):        
        
        if cur_sum == 0: return True
        
        if i == 0: return cur_sum == arr[0]
    
        if dp[cur_sum][i] != -1: return dp[cur_sum][i]
    
        take = False
        if cur_sum >= arr[i]: take = find(cur_sum - arr[i], i - 1)
        
        not_take = find(cur_sum, i - 1)
        
        dp[cur_sum][i] = take or not_take
        return dp[cur_sum][i]
    
    return find(target, n - 1)
```    
**TC: O(MxN)
SC: O(M+N) + O(MxN) for recursive stack and 2D dp array**

**Tabulation (Bottom-up)**
```
def subsetSumToK(n, target, arr):
    
    dp = [[False]*(target + 1) for _ in range(n)]
    
    for i in range(n): dp[i][0] = True
    if arr[0] <= target: dp[0][arr[0]] = True
    
    for i in range(1,n):
        for cur_sum in range(1,target + 1):
        
            take = False
            if cur_sum >= arr[i]: take = dp[i - 1][cur_sum - arr[i]]
            not_take = dp[i - 1][cur_sum]

            dp[i][cur_sum] = take or not_take
            
    return dp[n - 1][target]
```

**TC: O(MxN)
SC: O(MxN) for 2D dp array**


**Space optimized (Bottom-Up)**
```
def subsetSumToK(n, k, arr):
    
    prev = [False]*(k + 1)
    cur = [False]*(k + 1)
    prev[0] = cur[0] = True
    
    if arr[0] <= k: prev[arr[0]] = True
    
    for i in range(1,n):
        for target in range(1, k + 1):
            take = False
            if target >= arr[i]: take = prev[target - arr[i]]
            not_take = prev[target]

            cur[target] = take or not_take
        prev = cur[:]
        
    return cur[k]
```
**TC: O(MxN)
SC: O(N) for 1D dp array**
