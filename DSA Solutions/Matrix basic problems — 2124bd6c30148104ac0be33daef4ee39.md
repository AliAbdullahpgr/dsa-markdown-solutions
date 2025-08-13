# Matrix basic problems —>

Difficulty: basic
 : Yes
: June 14, 2025
Problem: matrix, theory, traversals
Time Taken: 1 hour+

Feels hard at first but they are simple to do if you understand matrices.

| Problem | Difficulty | Status |
| --- | --- | --- |
| Print Matrix Row-Wise and Column-Wise | Basic | remember an matrix is a 2d array with structure like array[row][col] |
| Calculate Total Sum of Matrix Elements | Basic | traverse through each elements of matrix and keep adding them |
| Calculate Sum of Each Row and Column | Basic | take a an array of size row take the sum of each row in each element of array |
| Find Max/Min Values in Each Row | Basic | use Min/max per each col/row |
| Find Max/Min Values in Each Column | Basic | use Min/max per each col/row |
| Add and Subtract Matrices | Basic | simple add n subtract but each elements of two matrices |
| Print Upper and Lower Triangle | Basic | if(j≥i)then upper if j≤i then lower triangle is printed |
| Print Left and Right Diagonals | Basic | if(i==j)or row==col then left diagonal is printed and row-col==0 if row is not equal to 0 right diagonal |
| Print Boundary Elements | Basic | row==0||col==0||row==m-1||col==n-1|| means to print the elements on the sides of edges |
| Sort Matrix Row-Wise and Column-Wise | Basic | use sort() for each row as sort(arr[i],arr[i]+row) in loop for row wise sort and for colum take a transpose of the array copy it in another array sort using the row logic and the do a reverse transpose |
| Print Matrix in Zig-Zag Pattern | Basic | use bool alt for alternating logic |
| Check if Matrix is Symmetric | Basic | arr[i][j]==arr[j][i] |
| Check if Matrix is Identity Matrix | Basic | check if arr[i][j]==1 at diagonals all other elements are 0 |
| Check if Matrix is Sparse | Basic | use a counter count the total number of zeros if the counter≥size of the matrix/2 then it’s a sparse matrix |
| Find Matrix Inverse | Basic | use determinent and divide it by adjacent of the matrix works for 2d matrix 3d matrix idk |