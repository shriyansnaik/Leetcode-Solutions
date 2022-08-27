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

