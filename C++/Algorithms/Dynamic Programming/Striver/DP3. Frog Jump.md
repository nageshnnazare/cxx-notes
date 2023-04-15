# Frog Jump

**References:**
[Striver](https://takeuforward.org/data-structure/dynamic-programming-frog-jump-dp-3/)
[gfg](https://practice.geeksforgeeks.org/problems/geek-jump/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=geek-jump)

---

**Problem Statement:**
Given a number of stairs and a frog, the frog wants to climb from the 0th stair to the (N-1) th stair. At a time the frog can climb either one or two steps. A height[N] array is also given. Whenever the frog jumps from a stair i to stair j, the energy consumed in the jump is abs(height[i]- height[j]), where abs() means the absolute difference. We need to return the minimum energy that can be used by the frog to jump from stair 0 to stair N-1.

---

**Solution**

_Recursive_

```c++
int minEnergy(int n, const std::vector<int>& cost){
 if (n == 0) return 0;

 int oneJump = minEnergy(n-1, cost) + abs(cost[n] - cost[n-1]);
 int twoJump = INT_MAX;
 if (n > 1)
  twoJump = minEnergy(n-2, cost) + abs(cost[n] - cost[n-2]);
 return min(oneJump, twoJump);
}

```

_Memoization_

```c++
int frogJump(int n, const std::vector<int>& cost){
 std::vector<int> dp(n+1, -1);
 return minEnergy(n, cost, dp);
}

int minEnergy(int n, const std::vector<int> &cost, std::vector<int >& dp){
 if (n == 0) return 0;
 if (dp != -1) return dp[n];

 int oneJump = minEnergy(n-1, cost, dp) + abs(cost[n] - cost[n-1]);
 int twoJump = INT_MAX;
 if (n > 1)
  twoJump = minEnergy(n-2, cost, dp) + abs(cost[n] - cost[n-2]);
 return dp[n] = min(oneJump, twoJump);
}
```

_Tabulation_

```c++
int minEnergy(int n, const std::vector<int>& cost){
 std::vector<int> dp(n+1, -1);
 dp[0] = 0;

 for(int i=1; i<n; i++) {
  int oneJump = dp[i-1] + abs(cost[i] - cost[i-1]);
  int twoJump = INT_MAX;
  if (i > 1)
   twoJump = dp[i-2] + abs(cost[i] - cost[i-2]);
  dp[i] = min(oneJump, twoJump);
 }
 return dp[n-1];
}
```

_Space Optimization_

```c++
int minEnergy(int n, const std::vector<int>& cost){
 int prev = 0, prev2 = 0;

 for(int i=1; i<n; i++) {
  int oneJump = prev + abs(cost[i] - cost[i-1]);
  int twoJump = INT_MAX;
  if (i > 1)
   twoJump = prev2 + abs(cost[i] - cost[i-2]);
  int curr = min(oneJump, twoJump);
  prev2 = prev;
  prev = curr;
 }
 return prev;
}
```

---
