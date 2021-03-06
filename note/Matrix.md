# Matrix

## Diagonal Transverse

+ elements at the same diagonal have the **same sum of x index and y index**

  <img src="C:\Users\yluo\AppData\Roaming\Typora\typora-user-images\image-20210405170949738.png" alt="image-20210405170949738" style="zoom:50%;" />

+ elements at the same anti-diagonal have the same **difference of x index and y index**

+ use `HashTable` to store element with same ordinates sum

#### Problems:

1. [Diagonal Transverse](https://leetcode.com/problems/diagonal-traverse/) 
2. [Diagonal Transverse II](https://leetcode.com/problems/diagonal-traverse-ii/)



## Rotate Image



## Spiral Transverse

+ use left, right, up and bottom **boundaries**



#### Problems

1. [Spiral Matrix](https://leetcode.com/problems/spiral-matrix/)
2. [Spiral Matrix II](https://leetcode.com/problems/spiral-matrix/)



## Search Sorted Matrix

Idea: elements on the right side are larger and elements on the top are smaller, then <u>search either from bottom left or top right</u>, **template**:

```java
public boolean searchMatrix(int[][] matrix, int target) {
        //search from either from bottom left corner or top right corner
        int height = matrix.length;
        if(height <= 0) return false;
        int width = matrix[0].length;
        int row = height - 1;
        int col = 0;
        while(row >= 0 && col < width){
            if(matrix[row][col] == target){
                return true;
            }else if(matrix[row][col] < target){
                col ++;
            }else{
                row --;
            }
        }
        return false;
    }
```

1. [74. Search a 2D Matrix -- Medium](https://leetcode.com/problems/search-a-2d-matrix/)
2. [240. Search a 2D Matrix II -- Medium](https://leetcode.com/problems/search-a-2d-matrix-ii/)
3. [378. Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/)



## Sub rectangle sum

[video tutorial](https://www.youtube.com/watch?v=yCQN096CwWM), basically try  sub rectangles with differnet **left boundary** and **right boundary**, then use **<u>Kadane's algorithm</u>** to find the maxSum and track the **upper boundary** and **lower boundary**

<img src="images/image-20210703224806916.png" alt="image-20210703224806916" style="zoom:50%;" />

#### problems

[304. Range Sum Query 2D - Immutable -- Medium](https://leetcode.com/problems/range-sum-query-2d-immutable/submissions/)

[363. Max Sum of Rectangle No Larger Than K --  Hard](https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/) need to think about another constraint, `maxSum <= k`

[85. Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/) **<u>*need review*</u>**



