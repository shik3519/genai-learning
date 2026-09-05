# LeetCode Cheat Sheet

| # | Problem | Pattern | Hint |
|---|---------|---------|------|
| 1 | Two Sum | Hash Map | Store `complement = target - n` in a dict as you iterate; return indices when complement is found |
| 3 | Longest Substring No Repeat | Sliding Window | Char→last-index map; when repeat found, jump `left` to one past the previous occurrence |
| 5 | Longest Palindromic Substring | Expand Around Center | For each index, expand outward for both odd (`i,i`) and even (`i,i+1`) centers while chars match |
| 8 | String to Integer (atoi) | String Parsing | 4 steps in order: skip spaces → read sign → read digits → clamp result to `[−2³¹, 2³¹−1]` |
| 9 | Palindrome Number | Math | Reverse only the second half of digits; compare with first half — avoids overflow |
| 11 | Container With Most Water | Two Pointers | Start pointers at both ends; move whichever side has the shorter height (it's the bottleneck) |
| 14 | Longest Common Prefix | Sort Trick | After sorting, only compare the lexicographic min and max — their LCP is the answer for all |
| 15 | 3Sum | Sort + Two Pointers | Sort; for each pivot `i`, two-pointer on `[i+1..end]` for complement; skip duplicate pivots and pointer values |
| 20 | Valid Parentheses | Stack | Push open brackets; on close bracket, check stack top matches — return false if mismatch or empty |
| 21 | Merge Two Sorted Lists | Linked List | Use a dummy head; at each step attach the smaller of the two current nodes; append remainder at end |
| 26 | Remove Duplicates (sorted) | Write Pointer | Write pointer starts at 1; advance only when `nums[i] != nums[i-1]`; return write index as new length |
| 33 | Search in Rotated Array | Binary Search | At each mid, one half is always sorted; check if target falls in that range, then discard the other half |
| 34 | First & Last Position | Binary Search | Run binary search twice — first biased left (keep going left on match), then biased right |
| 49 | Group Anagrams | Hash Map | `''.join(sorted(word))` is a canonical key shared by all anagrams; group words by this key |
| 53 | Maximum Subarray | Kadane's | `current = max(n, current + n)` — either start fresh or extend; `best = max(best, current)` |
| 56 | Merge Intervals | Greedy | Sort by start; if current start ≤ last merged end, extend end with `max`; otherwise append |
| 88 | Merge Sorted Arrays | Two Pointers | Write from the back (index `m+n-1`); compare from the ends of both arrays — no overwrite risk |
| 104 | Max Depth Binary Tree | DFS Recursion | `depth(node) = 1 + max(depth(left), depth(right))`; base case: `null → 0` |
| 121 | Best Time to Buy Stock I | Greedy | Track `min_price` seen so far; at each day `profit = price − min_price`; return max profit seen |
| 122 | Best Time to Buy Stock II | Greedy | You can trade every day — just sum up every positive day-to-day price difference |
| 125 | Valid Palindrome | Two Pointers | Shrink from both ends; skip non-alphanumeric chars; compare lowercase — return false on mismatch |
| 169 | Majority Element | Boyer-Moore Voting | Keep a candidate and count; increment on match, decrement on mismatch; reset candidate when count = 0 |
| 189 | Rotate Array | Three Reverses | Reverse entire array → reverse first `k` → reverse last `n−k`; achieves O(n) time, O(1) space |
| 198 | House Robber | DP (rolling) | `prev2, prev1 = prev1, max(prev1, prev2 + n)` — either rob current house or skip it |
| 215 | Kth Largest Element | Quickselect | Random pivot → partition → if pivot index matches target index return it; else recurse one side only |
| 217 | Contains Duplicate | Hash Set | Add each number to a set; if it's already there, return True immediately |
| 238 | Product Except Self | Prefix + Suffix | Left pass fills prefix products; right pass multiplies in suffix on the fly — no division, O(1) extra space |
| 242 | Valid Anagram | Frequency Count | `Counter(s) == Counter(t)` — same chars, same counts; also check lengths match first |
| 268 | Missing Number | Math | Expected sum `n*(n+1)//2` minus actual `sum(nums)` gives the missing number |
| 271 | Encode/Decode Strings | Length Prefix | Encode as `"<len>#<string>"`; decoder reads length, jumps past `#`, slices exactly that many chars |
| 283 | Move Zeroes | Write Pointer | Write non-zero elements forward in one pass; fill remaining positions with 0s in a second pass |
| 345 | Reverse Vowels | Two Pointers | Move left and right inward; skip non-vowels on each side; swap when both land on vowels |
| 347 | Top K Frequent | Bucket Sort | Count frequencies with Counter; bucket `bucket[freq]` holds numbers with that frequency; sweep top-down |
| 349 | Intersection of Arrays | Set / Two Pointers | `set(a) & set(b)` for O(m+n); if sorted: two pointers advance together on match, smaller side otherwise |
| 560 | Subarray Sum = K | Prefix Sum + Hash | Running sum; `count += seen[running − k]`; store `seen[running] += 1`; seed `seen[0] = 1` |
| 771 | Jewels and Stones | Hash Set | Put jewels in a set; count how many characters of stones appear in that set |
