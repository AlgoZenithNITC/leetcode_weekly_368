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



# Fourth Question - Minimum Changes to Make K Semi-palindromes

<details>
    <summary>Python Code</summary>

        class Solution:
            def minimumChanges(self, st: str, k: int) -> int:
                def num(st):
                    n = len(st)
                    ans = float('inf')
                    for it in fac[len(st)]:
                        nu = n // it
                        cur = 0
                        for i in range(nu // 2):
                            i2 = nu - i - 1
                            for j in range(it):
                                if st[i * it + j] != st[i2 * it + j]:
                                    cur += 1
                        ans = min(ans, cur)
                    return ans
        
                n = len(st)
                for i in range(2, n + 1):
                    fac[i] = []
                    for j in range(1, i):
                        if i % j == 0:
                            fac[i].append(j)
        
                dp = [[float('inf')] * (k + 1) for _ in range(n + 1)]
                dp[0][0] = 0
        
                for i in range(n):
                    for j in range(i + 1):
                        cur = st[j:i + 1]
                        add = num(cur)
                        for l in range(k):
                            dp[i + 1][l + 1] = min(dp[i + 1][l + 1], dp[j][l] + add)
        
                return dp[n][k]
              
        # Initialize the fac array.
        fac = [[] for _ in range(210)]


  
</details>


<details>
  <summary>C++</summary>

            class Solution {
                  public:
                      int dp[210][110];  // A 2D array to store dynamic programming values.
                      vector<int> fac[210];  // A vector of vectors to store factors of string lengths.
                  
                      // Function to calculate the number of changes needed to make a string palindrome.
                      int num(string st) {
                          int n = st.length();
                          int ans = 1e9;  // Initialize ans with a large value.
                  
                          // Iterate through all factors of the string length.
                          for (auto it : fac[st.length()]) {
                              int nu = n / it;
                              int cur = 0;
                  
                              // Compare characters in the string to make it a palindrome.
                              for (int i = 0; i < nu / 2; i++) {
                                  int i2 = nu - i - 1;
                                  for (int j = 0; j < it; j++)
                                      if (st[i * it + j] != st[i2 * it + j])
                                          cur++;
                              }
                  
                              ans = min(ans, cur);  // Update ans with the minimum changes needed.
                          }
                          return ans;
                      }
                  
                      // Main function to calculate the minimum changes needed.
                      int minimumChanges(string st, int k) {
                          int n = st.length();
                  
                          // Precompute factors for string lengths.
                          for (int i = 2; i <= n; i++)
                              for (int j = 1; j < i; j++)
                                  if (i % j == 0)
                                      fac[i].push_back(j);
                  
                          // Initialize the dp array with a large value.
                          for (int i = 0; i <= n; i++)
                              for (int j = 0; j <= k; j++)
                                  dp[i][j] = 1e9;
                  
                          dp[0][0] = 0;  // Base case: no changes needed for an empty string.
                  
                          // Dynamic programming to find the minimum changes needed.
                          for (int i = 0; i < n; i++)
                              for (int j = 0; j <= i; j++) {
                                  string cur = st.substr(j, i - j + 1);
                                  int add = num(cur);  // Calculate changes needed for the current substring.
                  
                                  // Update dp values for different values of k.
                                  for (int l = 0; l < k; l++)
                                      dp[i + 1][l + 1] = min(dp[i + 1][l + 1], dp[j][l] + add);
                              }
                  
                          return dp[n][k];  // Return the minimum changes needed for the entire string.
                      }
                  };

          
</details>


<details>
  <summary>JAVA</summary>


          public class Solution {
              int[][] dp = new int[210][110];
              List<Integer>[] fac = new List[210];
          
              public int num(String st) {
                  int n = st.length();
                  int ans = 1e9;
          
                  for (int it : fac[st.length()]) {
                      int nu = n / it;
                      int cur = 0;
          
                      for (int i = 0; i < nu / 2; i++) {
                          int i2 = nu - i - 1;
                          for (int j = 0; j < it; j++) {
                              if (st.charAt(i * it + j) != st.charAt(i2 * it + j)) {
                                  cur++;
                              }
                          }
                      }
          
                      ans = Math.min(ans, cur);
                  }
                  return ans;
              }
          
              public int minimumChanges(String st, int k) {
                  int n = st.length();
          
                  for (int i = 2; i <= n; i++) {
                      fac[i] = new ArrayList<>();
                      for (int j = 1; j < i; j++) {
                          if (i % j == 0) {
                              fac[i].add(j);
                          }
                      }
                  }
          
                  for (int i = 0; i <= n; i++) {
                      for (int j = 0; j <= k; j++) {
                          dp[i][j] = 1e9;
                      }
                  }
          
                  dp[0][0] = 0;
          
                  for (int i = 0; i < n; i++) {
                      for (int j = 0; j <= i; j++) {
                          String cur = st.substring(j, i - j + 1);
                          int add = num(cur);
          
                          for (int l = 0; l < k; l++) {
                              dp[i + 1][l + 1] = Math.min(dp[i + 1][l + 1], dp[j][l] + add);
                          }
                      }
                  }
          
                  return dp[n][k];
              }
          }


</details>
