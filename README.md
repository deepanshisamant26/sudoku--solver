# sudoku--solver

 Project on Sudoku solver
We know that Sudoku is a 9 x 9 number grid, and the whole grid are also divided into 3 x 3 boxes There are some rules to solve the Sudoku.

We have to use digits 1 to 9 for solving this problem.

One digit cannot be repeated in one row, one column or in one 3 x 3 box.
Technique Used:
  Backtracking
    Approach: 
  Sudoku can be solved by one by one assigning numbers to empty cells. Before assigning                    a number, check whether it is safe to assign. Check that the same number is not present in the current row, current column and current 3X3 subgrid. After checking for safety, assign the number, and recursively check whether this assignment leads to a solution or not. If the assignment doesn’t lead to a solution, then try the next number for the current empty cell. And if none of the number (1 to 9) leads to a solution, return false and print no solution exists.
Programming language used: C++
How can user run this project:
User need to input a valid sudoku for getting correct output.
The empty spaces should be assign to 0 .
About project:
solveSudoku(grid)//function
1.find empty position in the grid.
2.if not found return true.
3.if found,start exploring that position from 1 to 9
   * check for row
    *check for col
    *check for box
Function used:
*solveSudoku
*findEmptyPosition(for finding empty position)basically traversing the whole matrix if 0th position is found then it re-assigns the row and column to that position
*isSafe ( is the number is safe to be placed in matrix)
*isSafeInRow( is the number is safe to be placed in row)
*isSafeInCol( is the number is safe to be placed in col)
*isSafeInBox( is the number is safe to be placed in box)


Code:
#include<bits/stdc++.h>
using namespace std;
#define N 9
bool findEmptyPosition(int grid[N][N],int &row,int &col)
{
    for(int i=0;i<N;i++)
    {

        for(int j=0;j<N;j++)
        {
            if(grid[i][j]==0)
            {
                row=i;
                col=j;
                return true;
            }
        }
    }
    return false;
}
bool isSafeInRow(int grid[N][N],int row,int num)
{
    for(int i=0;i<N;i++)
        {
            if(grid[row][i]==num)
            {
                return false;
            }
        }
        return true;
}
bool isSafeInCol(int grid[N][N],int col,int num)
{
    for(int i=0;i<N;i++)
        {
            if(grid[i][col]==num)
            {
                return false;
            }
        }
        return true;
}
bool isSafeInBox(int grid[N][N],int row,int col,int num)
{
    int topLeftRow=row-(row%3);
    int topRightCol=col-(col%3);
    for(int i=0;i<3;i++)
    {
        for(int j=0;j<3;j++)
        {
            if(grid[i+topLeftRow][j+topRightCol]==num)
            {
                return false;
            }
        }
    }
    return true;
}
bool isSafe(int grid[N][N],int row,int col,int num)
{
   if(isSafeInRow(grid,row,num) && isSafeInCol(grid,col,num) && isSafeInBox(grid,row,col,num))
   {
       return true;
   }
   return false;
}
bool solveSudoku(int grid[N][N])
{
 int row,col;

 if(!findEmptyPosition(grid,row,col))
 {
     return true;
 }

 for(int i=1;i<=N;i++)

 {
     if(isSafe(grid,row,col,i))
     {
         grid[row][col]=i;
         if(solveSudoku(grid)){
            return true;
         }
         grid[row][col]=0;
     }
 }
return false;
}
int main()
{
    int grid[N][N];
    for(int i=0;i<N;i++)
    {
        string s;
        cin>>s;
        for(int j=0;j<s.length();j++)
        {
            grid[i][j]=s[j]-'0';
        }
    }
    solveSudoku(grid);
    cout<<endl;
    for(int i=0;i<N;i++)
   {
        for(int j=0;j<N;j++){
            cout<<grid[i][j]<<" ";
        }
        cout<<endl;
    }
}
Input:
0 5 0 3 1 4 0 6 0
8 7 0 0 0 9 4 0 3
6 4 3 5 0 7 1 9 2
0 0 7 8 0 5 2 1 0
4 1 0 9 0 0 0 0 0
0 2 5 0 6 1 9 0 7
7 9 0 2 5 0 8 4 0 
0 0 4 0 9 6 0 0 5 
0 3 0 1 0 8 6 7 0
Output:
2 5 9 3 1 4 7 6 8
8 7 1 6 2 9 4 5 3
6 4 3 5 8 7 1 9 2
9 6 7 8 3 5 2 1 4
4 1 8 9 7 2 5 3 6
3 2 5 4 6 1 9 8 7
7 9 6 2 5 3 8 4 1
1 8 4 7 9 6 3 2 5
5 3 2 1 4 8 6 7 9
