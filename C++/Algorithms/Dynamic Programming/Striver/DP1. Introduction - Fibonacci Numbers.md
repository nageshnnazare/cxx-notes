# Fibonacci numbers

0 1 1 2 3 5 8 13 21

`f(n) = f(n-1) + f(n-2)`

```c++
f(n) {
 if(n <= 1) return n;

 return f(n-1) + f(n-2);
}
```

f(4) = f(3) + f(2)

f(3) = f(2) + f(1) = (f(1) + f(0)) + f(1)
f(2) = f(1) + f(0)

Overlapping sub-problems

---

## Memoization

(Top-down Approach)
Store the value of subproblems in an array/ map/ table

```c++
std::vector<int> dp(n+1, -1);
f(int n, std::vector<int> &dp) {
 if(n <= 1) return n;
 if(dp[n] != -1) return dp[n];

 return dp[n] = f(n-1, dp) + f(n-2, dp);
}
```

Time complexity : O(n)
Space complexity : O(n) (recusion stack) + O(n) (dp array)

---

## Tabulation

(Bottom-up Approach)

```c++
f(int n) {
 std::vector<int> dp(n+1, -1);
 dp[0] = 0; d[1] = 1;

 for(int i=2; i<=n; i++) {
  dp[i] = dp[i-1] + dp[i-2];
 }
 return dp[n];
}
```

Time complexity : O(n)
Space complexity : O(n) (dp array)

---

## Improving Space Complexity

```c++
f(int n) {
 int curr = -1, prev = 1, prev2 = 0;

 for(int i=2; i<=n; i++) {
  curr = prev + prev2;
  prev2 = prev;
  prev = curr;
 }
 return prev;
}
```

Time complexity : O(n)
Space complexity : O(1)

---

### Intuition

1. Try to represent the problem in terms of index
2. Do all posibble stuffs on that index according to the problem statements
3. Sum up all stuffs (count all ways/ find min/ find max )

---
