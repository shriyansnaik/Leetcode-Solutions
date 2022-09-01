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
            
    return dp[n - 1]

def minSubsetSumDifference(arr, n):
    total = sum(arr)
    dp = subsetSumToK(n, total, arr)
    mini = float("inf")
    for cur_sum in range(len(dp)//2 + 1):
        if dp[cur_sum]: mini = min(mini, abs(2*cur_sum - total))
        
    return mini
```    
