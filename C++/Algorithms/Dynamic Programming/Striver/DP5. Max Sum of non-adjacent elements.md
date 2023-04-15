# Max Sum of non-adjacent elements

**References:**
[Striver](https://takeuforward.org/data-structure/maximum-sum-of-non-adjacent-elements-dp-5/)
[gfg](https://practice.geeksforgeeks.org/problems/max-sum-without-adjacents2430/1?utm_source=youtube&utm_medium=collab_striver_ytdescription&utm_campaign=max-sum-without-adjacents)

---

**Problem Statement:**
Given an array of ‘N’ positive integers, we need to return the maximum sum of the subsequence such that no two elements of the subsequence are adjacent elements in the array.

---

**Solution:**

_Recursive_

```c++
int f(int *arr, int n) {
 if( n == 0 ) return arr[n];
 if( n < 0 ) return 0;

 int pick = arr[n] + f(arr, n-2);
 int not_pick = 0 + f(arr, n-1);

 return max(pick, not_pick);
}

int findMaxSum(int *arr, int n) {
 return f(arr, n-1);
}
```

_Memoization_

```c++
int f(int *arr, int n, std::vector<int>& dp) {
 if( n == 0 ) return arr[n];
 if( n < 0 ) return 0;
 if( dp[n] != -1) return dp[n];

 int pick = arr[n] + f(arr, n-2, dp);
 int not_pick = 0 + f(arr, n-1, dp);

 return dp[n] = max(pick, not_pick);
}

int findMaxSum(int *arr, int n) {
 std::vector<int> dp(n, -1);
 return f(arr, n-1, dp);
}
```

_Tabulation_

```c++
int findMaxSum(int *arr, int n) {
 std::vector<int> dp(n+1, -1);
 dp[0] = 0;

 for(int i=1; i<n; i++) {
  int pick = arr[i];
  if(i > 1) pick += dp[i-2];
  int not_pick = 0 + dp[i-1];
  dp[i] = max(pick, not_pick);
 }
 return dp[n-1];
}
```

_Space Optimization_

```c++
int findMaxSum(int *arr, int n) {
 int prev = arr[0], prev2 = 0;

 for(int i=1; i<n; i++) {
  int pick = arr[i];
  if(i > 1) pick += prev2;
  int not_pick = 0 + prev;
  int curr = max(pick, not_pick);
  prev2 = prev;
  prev = curr;
 }
 return prev;
}
```

---
