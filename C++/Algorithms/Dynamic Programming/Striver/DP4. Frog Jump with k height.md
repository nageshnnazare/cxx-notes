# Frog Jump with k height

**References:**
[Striver](https://takeuforward.org/data-structure/dynamic-programming-frog-jump-with-k-distances-dp-4/)
[gfg](https://practice.geeksforgeeks.org/problems/minimal-cost/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=minimal-cost)

---

**Problem Statement:**
This is a follow-up question to “Frog Jump” discussed in the previous article. In the previous question, the frog was allowed to jump either one or two steps at a time. In this question, the frog is allowed to jump up to ‘K’ steps at a time. If K=4, the frog can jump 1,2,3, or 4 steps at every index.

---

**Solution:**

_Recursive_

```c++
int minimizeCost(vector<int>& height, int n, int k) {
 if (n == 0) return 0;
 int minCost = INT_MAX;
 for(int j=1; j<=k; j++) {
  if(n-j > 0) {
   int cost = minimizeCost(height, n-j, k) + (abs(height[n] - height[n-j]));
   minCost = min(cost, minCost);
  }
 }
 return minCost;
}
```

_Memoization_

```c++
int minimizeCost(vector<int>& height, int n, int k) {
 std::vector<int> dp(n+1, -1);
 return mCost(height, n, k, dp);
}

int mCost(vector<int>& height, int n, int k, dp) {
 if (n == 0) return 0;
 if (dp[n] != -1) return dp[n];

 int minCost = INT_MAX;
 for(int j=1; j<=k; j++) {
  if(n-j > 0) {
   int cost = minimizeCost(height, n-j, k) + (abs(height[n] - height[n-j]));
   dp[n] = minCost = min(cost, minCost);
  }
 }
 return dp[n];
}
```

_Tabulation_

```c++
int minimizeCost(vector<int>& height, int n, int k) {
 std::vector<int> dp(n+1, -1);
 dp[0] = 0;

 for(int i=1; i<n; i++) {
  int minCost = INT_MAX;
  for(int j=1; j<=k; j++) {
   if (i-j >= 0) {
    int cost = dp[i-j] + abs(height[i] - height[i-j]);
    minCost = min(minCost, cost);
   }
  }
  dp[i] = minCost;
 }
 return dp[n-1];
}
```

---
