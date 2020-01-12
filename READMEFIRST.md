# N-QueensProblem
A solution to the N-Queens Problem implemented in java
To get the project clone or download and open with Netbeans or intelli J

or just view source code here:

package n.queens.problem;
import java.util.Scanner;

/**
 *
 * @author eugeneikonya
 */
public class NQueensProblem {
   static int N;
   
   public static void printBoard(int board[][]){
       for(int i=0;i<N;i++ ){
           for(int j=0;j<N;j++){
               if(board[i][j]==1){
                   System.out.print("Q\t");
                   //if the value at current location is one it prints Q for the queen
               }
               else{
                   System.out.print("-\t");
                   //if the value is 0 it puts a dash
               }
               
           }
           System.out.println("\n");
       }
   }
   
   public static boolean checkPositions(int board[][],int row,int col){
       int i,j;
       //to check to the left of the position as they can only be in the left side
       //the function has a time complexity of O(N)
       for( i=0;i<col;i++)
       {
           if(board[row][i]==1)
           {
               return false;
           }
       }
       //to check the top left side
       for(i=row,j=col;j>=0  && i>=0;i--,j--)
       {
           if(board[i][j]==1)
           {
               return false;
           }
       }
       //to check the bottom left side of the board (diagonally)
       for(i=row,j=col;j>=0 && i<N;i++,j--)
       {
            if(board[i][j]==1)
           {
               return false;
           }
       }
   
   return true;
   }
   
   public static boolean solveBoard(int board[][],int col){
       if(col>=N)
       {
           return true;
       }
       for(int i=0;i<N;i++){
           //check if there are any attacking queens to decide whether to place or not to place
           if(checkPositions(board,i,col))
           {
              board[i][col]=1;
              if(solveBoard(board,col+1))
              {
                  return true;
                 
              }
              //The backtracking happens here
              board[i][col]=0;
           } 
       }    
   
   return false;
   }
    public static void main(String[] args) {
        System.out.println("Enter the Value of N");
        Scanner sc =new Scanner(System.in);
        N=sc.nextInt();
        int board[][]=new int[N][N];
        if(!solveBoard(board,0))
        {
          System.out.println("There is no solution for this problem");  
        }
        printBoard(board);
        
    }
    
}
