## 题目
```
    编写一个高效的算法来搜索 m x n 矩阵 matrix 中的一个目标值 target。
    
    该矩阵具有以下特性：
        * 每行的元素从左到右升序排列。
        * 每列的元素从上到下升序排列。
```

### 示例:
```
    现有矩阵 matrix 如下：
    [
      [ 1,  4,  7, 11, 15],
      [ 2,  5,  8, 12, 19],
      [ 3,  6,  9, 16, 22],
      [10, 13, 14, 17, 24],
      [18, 21, 23, 26, 30]
    ]
    
    给定 target = 5，返回 true。
    给定 target = 20，返回 false。
```

### 解题思路
```
   方法一：
        从左下角为出发点，若小于目标，则向右；若大于目标，则向上
   方法二：
        每行做二分法查询
```

### 代码实现
```
   方法一：
   
   /**
    * @param {number[][]} matrix
    * @param {number} target
    * @return {boolean}
    */
   var searchMatrix = function(matrix, target) {
       let row = matrix.length - 1;
       let col = 0;
       while(row >=0 && col <= matrix[0].length - 1){
           if(matrix[row][col] == target){
               return true;
           }else if(matrix[row][col] < target){
               col++;
           }else if(matrix[row][col] > target){
               row--;
           }
       }
       return false;
   };
   
   方法二：
   /**
    * @param {number[][]} matrix
    * @param {number} target
    * @return {boolean}
    */
   var searchMatrix = function(matrix, target) {
       
       // 起始行
       let row_start = 0;
       // 结束行
       let row_end = matrix.length - 1;
       
       while(row_start < row_end){
           // 中间行
           let mid = row_start + (row_end - row_start)/2;
           
           if(matrix[mid][0] == target){
              return true;
           }else if(matrix[mid][0] > target){
              row_end = mid;
           }else if(matrix[mid][0] < target){
              row_start = mid + 1;
           }
       }
       // 可能在哪行
       let link = row_start - 1;
       if(link <= 0){
           return false;   
       }
       
       let col_start = 0;
       let col_end = matrix[0].length - 1;
       while(col_start < col_end){
           // 中间列
           let mid = col_start + (col_end - col_start)/2;
           
           if(matrix[link][mid] == target){
              return true;
           }else if(matrix[link][mid] > target){
              col_end = mid;
           }else if(matrix[link][mid] < target){
              col_start = mid + 1;
           }
       }
   
       return false;
   };
```