# Spiral Order Matrix

Input

```cpp
[ [1, 2, 3], [4, 5, 6], [7, 8, 9] ]
```

Output

```cpp
[1, 2, 3, 6, 9, 8, 7, 4, 5]
```

Solution

```cpp
	vector<int> Solution::spiralOrder(const vector<vector<int> > &A) {
    int m = A.size(), n = A[0].size();
    int T = 0, B = m - 1, L = 0, R = n - 1; // top, bottom ...
    int dir = 0;
    
    vector<int> ans;
    
    while (T <= B && L <= R) {
        if (dir == 0) {
            for (int i = L; i <= R; i++)
                ans.push_back(A[T][i]);
            T++;
            dir = 1;
        } else if (dir == 1) {
            for (int i = T; i <= B; i++)
                ans.push_back(A[i][R]);
            R--;
            dir = 2;
        } else if (dir == 2) {
            for (int i = R; i >= L; i--)
                ans.push_back(A[B][i]);
            B--;
            dir = 3;
        } else if (dir == 3) {
            for (int i = B; i >= T; i--)
                ans.push_back(A[i][L]);
            L++;
            dir = 0;
        }
    }
    
    return ans;
}
```
