## Insertion sort
* Algorithm
  * Input: nums array
  * For each item at position i:
    * While item at i-1 > item at i:
      * Swap items between i-1 and i
  * Output: nums array
  ```
  def insertion(nums):
      n = len(nums)
      for i in range(1, n):
          j = i
          while j > 0 and nums[j-1] > nums[j]:
              nums[j-1], nums[j] = nums[j], nums[j-1]
              j -= 1
      return nums
  ```
* Complexity analysis
  * Time complexity: n-1 steps in the loop; maximum of n-1 compare and swap in each step. Therefore,
    * T(n) = T(n-1) * T(n-1) = O(n^2)
  * Space complexity: in-place. O(1)


## Merge Sort
* Algorithm
  * Input: nums array
  * func mergeSort(nums):
    * left, right = divide(nums)
    * left = mergeSort(left)
    * right = mergeSort(right)
    * mergedSorted = merge(left, right)
  * Output: mergedSorted
  ```
  def mergeSort(nums):
      if len(nums) <= 1: return nums
      
      def divide(nums):
          mid = len(nums) // 2
          left = nums[:mid]
          right = nums[mid:]
          return left, right
          
      def merge(left, right):
          nLeft = len(left)
          nRight = len(right)
          mergedSorted = []
          i, j = 0, 0
          while i < nLeft or j < nRight:
              vLeft = left[i] if i < nLeft else float('inf')
              vRight = right[j] if j < nRight else float('inf')
              if vLeft < vRight:
                  mergedSorted.append(vLeft)
                  i += 1
              else:
                  mergedSorted.append(vRight)
                  j += 1
          return mergedSorted
      
      left, right = divide(nums)
      left = mergeSort(left)
      right = mergeSort(right)
      mergedSorted = merge(left, right)
      return mergedSorted
  ```
  
  * Complexity analysis
  * Time complexity: Consider a tree with
    * T(n) = O(1) + 2T(n/2) * O(n), i.e. divide + merge sort + merge = O(n log n)
    * Explanation:
      * At level 0, total number of operations = n
      * At level 1, total number of operations = n/2 + n/2 = n
      * At level 2, total number of operations = n/4 + n/4 + n/4 + n/4 = n
      * ...
      * At final level, total number of operations = 1 + 1 + ... + 1 = n
      * Number of levels = height or depth of the tree = 1 + log n
      * Therefore, O( (1 + log n) * n ) = O(n log n)
  * Space complexity: Auxiliary space required for left and right arrays, so O(n).