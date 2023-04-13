# Climbing Stairs

**References:**
[Striver](https://takeuforward.org/data-structure/dynamic-programming-climbing-stairs/)
[leetcode](https://leetcode.com/problems/climbing-stairs/)
[gfg](https://practice.geeksforgeeks.org/problems/count-ways-to-reach-the-nth-stair-1587115620/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=count-ways-to-reach-the-nth-stair-1587115620)

---

**Problem Statement:**
Given a number of stairs. Starting from the 0th stair we need to climb to the “Nth” stair. At a time we can climb either one or two steps. We need to return the total number of distinct ways to reach from 0th to Nth stair.

---

**Solution:**

_Recursive_

```c++
int climbStairs(int n){
 std::vector<int> dp(n+1, -1);
 return numWays(n, dp);
}

int numWays(int n, std::vector<int>& dp) {
 if(n==0 || n==1) return 1;
 if(dp[n] != -1) return dp[n];

 int oneSteps = numWays(n-1);
 int twoSteps = numWays(n-2);
 return dp[n] = oneSteps + twoSteps;
}
```

_Tabulation_

```c++
int climbStairs(int n){
 std::vector<int> dp(n+1, -1);
 dp[0] = dp[1] = 1;

 for(int i=2; i<=n; i++) {
  dp[i] = dp[i-1] + dp[i-2];
 }
 return dp[n];
}
```

_Space Optimization_

```c++
int climbStairs(int n){
 int prev = 1, prev2 = 1;

 for(int i=2; i<=n; i++) {
  int curr = prev + prev2;
  prev2 = prev;
  prev = curr;
 }
 return prev;
}
```

---
