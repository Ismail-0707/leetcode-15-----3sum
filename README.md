# LeetCode 15 - 3Sum

## Optimal Approach (Sorting + Two Pointers)

### Idea

1. Sort the array.
2. Fix one element `nums[i]`.
3. Use two pointers:
   - `left = i + 1`
   - `right = n - 1`
4. Find two numbers such that:

   nums[i] + nums[left] + nums[right] = 0

5. Skip duplicate elements to avoid duplicate triplets.

---

## Java Code

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();

        Arrays.sort(nums);

        for (int i = 0; i < nums.length - 2; i++) {

            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }

            int left = i + 1;
            int right = nums.length - 1;

            while (left < right) {

                int sum = nums[i] + nums[left] + nums[right];

                if (sum == 0) {

                    res.add(Arrays.asList(nums[i], nums[left], nums[right]));

                    while (left < right && nums[left] == nums[left + 1]) {
                        left++;
                    }

                    while (left < right && nums[right] == nums[right - 1]) {
                        right--;
                    }

                    left++;
                    right--;
                }
                else if (sum < 0) {
                    left++;
                }
                else {
                    right--;
                }
            }
        }

        return res;
    }
}
```

---

## Dry Run

Input:

```text
[-1,0,1,2,-1,-4]
```

After Sorting:

```text
[-4,-1,-1,0,1,2]
```

### i = 0 (-4)

```text
left = 1, right = 5
sum = -4 + (-1) + 2 = -3
Move left

sum = -4 + (-1) + 2 = -3
Move left

sum = -4 + 0 + 2 = -2
Move left

sum = -4 + 1 + 2 = -1
Move left
```

No triplet found.

### i = 1 (-1)

```text
left = 2, right = 5
sum = -1 + (-1) + 2 = 0
Triplet = [-1,-1,2]

left++, right--

sum = -1 + 0 + 1 = 0
Triplet = [-1,0,1]
```

Answer:

```text
[[-1,-1,2],[-1,0,1]]
```

---

## Complexity Analysis

Time Complexity: O(n²)

Space Complexity: O(1) (excluding output list)

---

## Key Insight

Sorting allows us to use the Two Pointer technique. For each fixed element, we efficiently search for the remaining two numbers in O(n), reducing the overall complexity from O(n³) to O(n²).
