# leetcodeWeekly368

# First Question
<details>

  <summary>Python CODE</summary>
METHOD ONE 

```
class Solution:
    def differenceOfSums(self, n: int, m: int) -> int:
        intList = [i for i in range(1, n+1)]
        divisible = notDivisible = 0
        for num in intList:
            if num%m == 0:
                divisible += num
            else:
                notDivisible += num
        return notDivisible - divisible
```
METHOD 2

```

class Solution:
    def differenceOfSums(self, n: int, m: int) -> int:
        totalSum = n*(n+1)//2
        loop = n//m
        mSum = 0
        while loop:
            totalSum -= loop*m
            mSum += loop*m
            loop-= 1
        return totalSum - mSum
```

</details>

<details>
  <summary>C++</summary>
  
  ```
      class Solution {
        public:
            int differenceOfSums(int n, int m) {
                int s1=0,s2=0;
                for(int i=1;i<=n;i++)
                {
                    if(i%m==0) s2+=i;
                    else s1+=i;
                }
                return s1-s2;
            }
    };
  ```

</details>


<details>
  <summary>JAVA</summary>
  
  ```
    public class Solution {
        public int differenceOfSums(int n, int m) {
            int s1=0,s2=0;
            for(int i=1;i<=n;i++)
            {
                if(i%m==0) s2+=i;
                else s1+=i;
            }
            return s1-s2;
        }
    }
  ```
</details>


# Second Question - Minimum Sum of Mountain Triplets II

<details>
    <summary>Python Code</summary>
  
  ```
    class Solution:
        def minimumSum(self, nums):
            m = float('inf')
            n = len(nums)
            l = [0] * n
            r = [0] * n
            l[0] = 0
            
            for i in range(1, n):
                if nums[l[i - 1]] < nums[i]:
                    l[i] = l[i - 1]
                else:
                    l[i] = i
            
            r[n - 1] = n - 1
            for i in range(n - 2, -1, -1):
                if nums[r[i + 1]] < nums[i]:
                    r[i] = r[i + 1]
                else:
                    r[i] = i
            
            for i in range(n):
                if nums[l[i]] < nums[i] and nums[i] > nums[r[i]] and l[i] < i and i < r[i]:
                    m = min(m, nums[i] + nums[l[i]] + nums[r[i]])
            
            if m == float('inf'):
                return -1
            return m

  ```
</details>


<details>
  <summary>C++</summary>
  
  ```
    class Solution {
        public:
            int minimumSum(vector<int>& nums) {
                int m = INT_MAX;
                int n = nums.size();
                vector<int> l(n),r(n);
                l[0]=0;
                for(int i=1;i<n;i++)
                {
                    if(nums[l[i-1]]<nums[i])
                    {
                        l[i]=l[i-1];
                    }
                    else l[i]=i;
                }
                r[n-1]=n-1;
                for(int i=n-2;i>=0;i--)
                {
                    if(nums[r[i+1]]<nums[i])
                    {
                        r[i]=r[i+1];
                    }
                    else r[i]=i;
                }
                for(int i=0;i<n;i++)
                {
                    if(nums[l[i]]<nums[i] && nums[i]>nums[r[i]] && l[i]<i && i<r[i])
                    {
                        m=min(m,nums[i]+nums[l[i]]+nums[r[i]]);
                    }
                }
                if(m==INT_MAX) return -1;
                return m;
            }
        };
  ```
</details>


<details>
  <summary>JAVA</summary>
  
  ```
        class Solution {
              public int minimumSum(int[] nums) {
                  int m = Integer.MAX_VALUE;
                  int n = nums.length;
                  int[] l = new int[n];
                  int[] r = new int[n];
                  l[0] = 0;
                  
                  for (int i = 1; i < n; i++) {
                      if (nums[l[i - 1]] < nums[i]) {
                          l[i] = l[i - 1];
                      } else {
                          l[i] = i;
                      }
                  }
                  
                  r[n - 1] = n - 1;
                  for (int i = n - 2; i >= 0; i--) {
                      if (nums[r[i + 1]] < nums[i]) {
                          r[i] = r[i + 1];
                      } else {
                          r[i] = i;
                      }
                  }
                  
                  for (int i = 0; i < n; i++) {
                      if (nums[l[i]] < nums[i] && nums[i] > nums[r[i]] && l[i] < i && i < r[i]) {
                          m = Math.min(m, nums[i] + nums[l[i]] + nums[r[i]]);
                      }
                  }
                  
                  if (m == Integer.MAX_VALUE) {
                      return -1;
                  }
                  return m;
              }
          }
  ```
</details>



# Third Question

<details>
    <summary>Python Code</summary>
  
      class Solution:

        def minOperations(self, s1: str, s2: str, x: int) -> int:
            n = len(s1)
            v = []
            for i in range(n):
                if s1[i] != s2[i]:
                    v.append(i)
            m = len(v)
            if m % 2 != 0:
                return -1
            dp = [[-1 for _ in range(m)] for _ in range(m)]
            ans = self.solve(0, m - 1, m, v, x, dp)
            return ans
    
        def solve(self, i, j, n, v, x, dp):
            if i >= n or j < 0 or i > j:
                return 0
            if dp[i][j] != -1:
                return dp[i][j]
            a = v[i + 1] - v[i] + self.solve(i + 2, j, n, v, x, dp)
            b = v[j] - v[j - 1] + self.solve(i, j - 2, n, v, x, dp)
            c = x + self.solve(i + 1, j - 1, n, v, x, dp)
            dp[i][j] = min(a, b, c)
            return dp[i][j]
</details>


<details>
  <summary>C++</summary>
  
  ```
  
    class Solution
    {
      public:
          int dp[501][501];
  
          int solve(int i, int j, int n, vector<int> &v, int x)
          {
              if (i >= n || j < 0 || i > j)
                  return 0;
              if (dp[i][j] != -1)
                  return dp[i][j];
              int a = v[i + 1] - v[i] + solve(i + 2, j, n, v, x);
              int b = v[j] - v[j - 1] + solve(i, j - 2, n, v, x);
              int c = x + solve(i + 1, j - 1, n, v, x);
              return dp[i][j] = min({a, b, c});
          }
  
          int minOperations(string s1, string s2, int x)
          {
              int n = s1.size();
              vector<int> v;
              for (int i = 0; i < n; i++)
              {
                  if (s1[i] != s2[i])
                      v.push_back(i);
              }
              memset(dp, -1, sizeof(dp));
              int m = v.size();
              if (m % 2 != 0)
                  return -1;
              int ans = solve(0, m - 1, m, v, x);
              return ans;
          }
    };
    
  ```

</details>


<details>
  <summary>JAVA</summary>
  
  ```
      class Solution {
        public int minOperations(String s1, String s2, int x) {
            int n = s1.length();
            List<Integer> v = new ArrayList<>();
            for (int i = 0; i < n; i++) {
                if (s1.charAt(i) != s2.charAt(i)) {
                    v.add(i);
                }
            }
            int m = v.size();
            if (m % 2 != 0) {
                return -1;
            }
            int[][] dp = new int[m][m];
            int ans = solve(0, m - 1, m, v, x, dp);
            return ans;
        }
  
        private int solve(int i, int j, int n, List<Integer> v, int x, int[][] dp) {
            if (i >= n || j < 0 || i > j) {
                return 0;
            }
            if (dp[i][j] != 0) {
                return dp[i][j];
            }
            int a = v.get(i + 1) - v.get(i) + solve(i + 2, j, n, v, x, dp);
            int b = v.get(j) - v.get(j - 1) + solve(i, j - 2, n, v, x, dp);
            int c = x + solve(i + 1, j - 1, n, v, x, dp);
            dp[i][j] = Math.min(a, Math.min(b, c));
            return dp[i][j];
        }
    }
  ```
</details>



# Fourth Question

<details>
    <summary>Python Code</summary>

    class Solution:
    def maxSum(self, n: list[int], k: int) -> int:
        mod = 10**9 + 7
        binaryArr = [0] * 31
        for x in n:
            for i in range(31):
                if x & (1 << i):
                    binaryArr[i] += 1
        r = 0
        while sum(binaryArr) and k:
            c = 0
            k -= 1
            for i in range(31):
                if binaryArr[i]:
                    binaryArr[i] -= 1
                    c += 1 << i
            r += c * c
            r %= mod
        return r

</details>


<details>
  <summary>C++</summary>

</details>


<details>
  <summary>JAVA</summary>

</details>
