# \* Leetcode: Leftmost One     :BLOG:Basic:


---

Leftmost One  

---

Similar Problems:  
-   [First Bad Version](https://code.dennyzhang.com/first-bad-version)
-   [Review: Binary Search Problems](https://code.dennyzhang.com/review-binarysearch)
-   Tag: [#binarysearch](https://code.dennyzhang.com/tag/binarysearch)

---

Given a 2D array, and each line has only 0 and 1, the front part is 0, and the latter part is 1. Find the number of columns in the leftmost 1 of all the rows in the array.  

Notice  
-   The number of rows in the array and the number of columns do not exceed 1000
-   In order to limit the time complexity, your program will run 50000 times

Example  
Given arr = [[0,0,0,1],[1,1,1,1]], return 0.  

    Explanation:
    Arr[1][0] is the leftmost 1 in all rows and its column is 0.

Given arr = [[0,0,0,1],[0,1,1,1]], return 1.  

    Explanation:
    Arr[1][1] is the leftmost 1 in all rows and its column is 1.

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/leftmost-one)  

Credits To: [leetcode.com](https://leetcode.com/problems/leftmost-one/description/)  

Leave me comments, if you have better ways to solve.  

    ## Blog link: https://code.dennyzhang.com/leftmost-one
    class Solution:
        """
        @param arr: The 2-dimension array
        @return: Return the column the leftmost one is located
        """
        def getColumn(self, arr):
            ## Basic Ideas: binary search
            ## Complexity: Time O(m*log(n)), Space O(1)
            row_count = len(arr)
            if row_count == 0: return 0
            col_count = len(arr[0])
            leftmost = row_count
            for i in range(row_count):
                # binarysearch
                l, r = 0, col_count-1
                while l<r:
                    # find first 1
                    m = int(l+(r-l)/2)
                    if arr[i][m] == 1:
                        r = m
                    else:
                        l = m + 1
                if arr[i][r] == 1:
                    leftmost = min(leftmost, r)
                else:
                    leftmost = min(leftmost, r+1)
            return leftmost