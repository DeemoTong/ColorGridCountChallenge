# Continuous Color Grid Count Challenge

This Java program will analyse a given color grid, and find out the largest continuous color block in the given grid.

## Run
To run this program, you need have at least Java 8.0 installed.

1. Use cmd in Windows or terminal in MacOS,Linux 
   

2. ```bash
    cd "your file directory"
    ```
3. ```bash
    java ColorGridCount
    ```

Or you can just run in to a compiler

## Test
Once you have compiled and run the program, you will be ask
```bash
Please input N, X ,Y
```
Input number you want to test, N is number of colors, X is number of rows, Y is number of columns.

For example:
```bash
Please input N, X ,Y
3
5
5
```

## Analysis

Since I need to calculate the largest color area in a given matrix, which means that I need to traverse each area in the matrix, I use Breadth First Search, which will traverse all the nodes through This feature allows me to quickly lock the largest area of the same color.

1. First we need to create a matrix,and I randomize the color of each region in the matrix
   ```java
   //Create a matrix
       ColorGrid(int n, int x, int y) {
        N = n;
        X = x;
        Y = y;
        grid = new int[X][Y];
        createGame();
    }
    //randomize the color
       private void createGame() {
        for (int i = 0; i < X; ++i) {
            for (int j = 0; j < Y; ++j) {
                grid[i][j] = (int) (Math.random() * N + 1);
            }
        }
    }
    ```
2. Then print it out through the method 
    ```java     
    printGame()
    ```
3. Find the largest area of the same color
   1.   First declare a **flag** to used to determine whether it has been traversed, and initialize a **maxCount** to record the maximum value of the same color area
        ```java
        int[][] flag = new int[X][Y];
        int maxCount = 0;
        List<List<Integer>> maxBlock = new ArrayList<>();
        ```
    2. I will traverse from the starting point in the two-dimensional array, and use **curBlock** to record the value of the current color.
    
        **directions** is to judge the four directions, which are the neighbors on the left, top, bottom and right of the current value, so as to to iterate over whether the neighbors of the current value have the same color.
        ```java
         int[][] directions = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
        ```

       When looking for the largest area of the same color, it must also satisfy the node that has neighbors, the node has not been traversed, and the color is the same as the color of the current node
        ```java
        if (newr >= 0 && newr < X && newc >= 0 && newc < Y
            && flag[newr][newc] == 0 && grid[newr][newc] == grid[r][c])
        ```
    3. Finally, after traversing all nodes, the maximum value is found
        ```java
        if(curBlock.size() > maxCount) {
            maxCount = curBlock.size();
            maxBlock = curBlock;
        }
        ```
## Output example

```cmd
C:\Users\>java ColorGridCount
Please input N, X, Y
3
5
5
Sample game printed on console
2, 3, 2, 1, 3
1, 3, 1, 1, 2
3, 1, 2, 1, 2
2, 1, 3, 1, 3
3, 1, 2, 2, 2

Sample game with largest continous block (LCB) marked by '0' symbol
Largest Continous Block Count: 5
2, 3, 2, 0, 3
1, 3, 0, 0, 2
3, 1, 2, 0, 2
2, 1, 3, 0, 3
3, 1, 2, 2, 2
```
