# leetcodeWeekly368

# First Question
<details>

  <summary>Python CODE</summary>
	BRUTE FORCE

```python
	class Solution:
		def minimumSum(self, nums):
			sum = float('inf')
			for i in range(len(nums) - 2):
				for j in range(i + 1, len(nums) - 1):
					for k in range(j + 1, len(nums)):
						if nums[i] < nums[j] and nums[j] > nums[k]:
							sum = min(sum, nums[i] + nums[j] + nums[k])
			return -1 if sum == float('inf') else sum
```

</details>

<details>
  <summary>C++</summary>
  
  ```cpp
    class Solution {
		public:
			int minimumSum(vector<int>& nums) {
				int sum = INT_MAX;
				for (int i = 0; i < nums.size() - 2; i++) {
					for (int j = i + 1; j < nums.size() - 1; j++) {
						for (int k = j + 1; k < nums.size(); k++) {
							if (nums[i] < nums[j] && nums[j] > nums[k])
								sum = min(sum, nums[i] + nums[j] + nums[k]);
						}
					}
				}
				return sum==INT_MAX?-1:sum;
			}
		};
  ```

</details>


<details>
  <summary>JAVA</summary>
  
  ```java
	class Solution {
		public int minimumSum(int[] nums) {
			int sum = Integer.MAX_VALUE;
			for (int i = 0; i < nums.length - 2; i++) {
				for (int j = i + 1; j < nums.length - 1; j++) {
					for (int k = j + 1; k < nums.length; k++) {
						if (nums[i] < nums[j] && nums[j] > nums[k]) {
							sum = Math.min(sum, nums[i] + nums[j] + nums[k]);
						}
					}
				}
			}
			return (sum == Integer.MAX_VALUE) ? -1 : sum;
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

```py
	class Solution:
		def possibleGroupSize(self, m, i):
			for key, value in m.items():
				no_groups_i_sized = value // i
				mem_not_in_groups = value % i
				if mem_not_in_groups < i - 1:
					req = (i - 1) - mem_not_in_groups
					if no_groups_i_sized >= req:
						mem_not_in_groups = i - 1
				if mem_not_in_groups > 0 and mem_not_in_groups < i - 1:
					return False
			return True

		def minGroupsForValidAssignment(self, nums):
			m = defaultdict(int)
			for num in nums:
				m[num] += 1
			min_freq = float('inf')
			for freq in m.values():
				min_freq = min(freq, min_freq)
			for i in range(min_freq + 1, 0, -1):
				if self.possibleGroupSize(m, i):
					no_of_groups = 0
					for val in m.values():
						mem_not_in_groups = val % i
						no_of_groups += val // i
						if mem_not_in_groups > 0:
							no_of_groups += 1
					return no_of_groups
			return -1
```
</details>


<details>
  	<summary>C++</summary>
  
```cpp
    class Solution {
        bool possibleGroupSize(unordered_map<int, int> &m, int i) {
            for (auto elem : m) {
                int no_groups_i_sized = elem.second / i,
                mem_not_in_groups = elem.second % i;
                if (mem_not_in_groups < i - 1) {
                    /* 
                    * if the members remaining are not i-1 sized
                    * they can't be a group. So assign the req 
                    * members for making it a i - 1 sized from 
                    * i sized groups to the remaining members
                    */
                    int req = (i - 1) - mem_not_in_groups;
                    if (no_groups_i_sized >= req)
                        mem_not_in_groups = i - 1;
                    // Total groups will be previous i sized groups
                    // plus new group that can be formed by borrowing
                }
                // after distributing the groups
                if (mem_not_in_groups > 0 && mem_not_in_groups < i - 1) {
                    return false;
                }
            }
            // we reach here iff we have arranged groups according to constraints
            // so return true
            return true;
        }
    public:
        int minGroupsForValidAssignment(vector<int>& nums) {
            unordered_map<int, int> m;
            for (int i = 0; i < nums.size(); i++) {
                m[nums[i]]++;
            }
            int min_freq = INT_MAX;
            for (auto a : m) {
                min_freq = min(a.second, min_freq);
            }
            for (int i = min_freq + 1; i > 0; i--) {
                if (possibleGroupSize(m, i)) {
                    // if groups with given size is possible
                    // count the no. of groups
                    int no_of_groups = 0;
                    for (auto k : m) {
                        int mem_not_in_groups = k.second % i;
                        no_of_groups += k.second / i;
                        // if there are any remaining members
                        // we know that the group formation 
                        // is possible so add the extra group
                        if (mem_not_in_groups > 0)
                            no_of_groups++;
                    }
                    // if group size is more no. of groups will
                    // be less
                    return no_of_groups;
                }
            }
            return -1;
        }
    };
```
</details>


<details>
	<summary>JAVA</summary>
  
```java
    class Solution {
        boolean possibleGroupSize(HashMap<Integer, Integer> m, int i) {
            for (HashMap.Entry<Integer, Integer> entry : m.entrySet()) {
                int no_groups_i_sized = entry.getValue() / i;
                int mem_not_in_groups = entry.getValue() % i;
                if (mem_not_in_groups < i - 1) {
                    int req = (i - 1) - mem_not_in_groups;
                    if (no_groups_i_sized >= req) {
                        mem_not_in_groups = i - 1;
                    }
                }
                if (mem_not_in_groups > 0 && mem_not_in_groups < i - 1) {
                    return false;
                }
            }
            return true;
        }

        public int minGroupsForValidAssignment(int[] nums) {
            HashMap<Integer, Integer> m = new HashMap<>();
            for (int num : nums) {
                m.put(num, m.getOrDefault(num, 0) + 1);
            }
            int min_freq = Integer.MAX_VALUE;
            for (int freq : m.values()) {
                min_freq = Math.min(freq, min_freq);
            }
            for (int i = min_freq + 1; i > 0; i--) {
                if (possibleGroupSize(m, i)) {
                    int no_of_groups = 0;
                    for (int val : m.values()) {
                        int mem_not_in_groups = val % i;
                        no_of_groups += val / i;
                        if (mem_not_in_groups > 0) {
                            no_of_groups++;
                        }
                    }
                    return no_of_groups;
                }
            }
            return -1;
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
