# Tictactoe
import java.util.*; 
public class PlayerMoves {
    private static String playerX = "X";
    private static String playerO = "O";
    private static char player1;
    private static char player2;
    private static int row;
    private static int col;
    private static char[][] boardMoves = GameBoard.createBoard();   
    public static void host(){
        Scanner scan = new Scanner(System.in);
    //I know all this is suppose to be in the main class, but i was too far into the project when i realized and i will get confused while switching all the variables and method. 
        System.out.println("What player do you want to be?");
        System.out.println(playerX + " or " + playerO);
            String choice = scan.nextLine();
        
           while(checkPlayer(choice)){
               System.out.println("Please pick X or O.");
               choice = scan.nextLine();
           }
               

            if(choice.equals(playerX)){
                System.out.println("You are player X.");
                player1 = playerX.charAt(0);
                System.out.println("Player 2 is player O.");
                player2 = playerO.charAt(0);
               
                    
            }
            if(choice.equals(playerO)) {
                System.out.println("You are player O.");
                player1 = playerO.charAt(0);
                System.out.println("Player 2 is player X.");
                player2 = playerX.charAt(0);
               
            }
            
            printMethod(GameBoard.createBoard());
            
            System.out.println("What is your move? Choose your location." + "(row, column)");
            System.out.println("1 = 1,1    2 = 1,3    3 = 1,5    4 = 3,1    5 = 3,3    6 = 3,5    7 = 5,1    8 = 5,3   9 = 5,5");
            while(true){
                    System.out.println("What is player 1's move?");
                    System.out.println("What is your row?");
                        row = scan.nextInt();
                    System.out.println("What is your column?");
                        col = scan.nextInt();
                while(checkMoves(row , col))
                {
                    System.out.println("That slot is already taken or out of bounds, please try again.");
                        printMethod(boardMoves);
                    System.out.println("What is your row?");
                        row = scan.nextInt();
                    System.out.println("What is your column?");
                        col = scan.nextInt();
                }
                changeboard(player1, row ,col);
                printMethod(boardMoves);
                if(checkWinner()){
                    System.out.println("The winner is player1.");
                        break;
                }
                if(checkTie()){
                    System.out.println("This is game is a tie.");
                        break;
                }
                
                System.out.println("What is player 2's move?");
                System.out.println("What is your row?");
                    row= scan.nextInt();
                System.out.println("What is your column?");
                    col = scan.nextInt();
                while(checkMoves(row, col))
                {
                    System.out.println("That slot is already taken, out of bounds, or an invaild move. Please try again.");
                    printMethod(boardMoves);
                    System.out.println("What is your row?");
                        row = scan.nextInt();
                    System.out.println("What is your column?");
                        col = scan.nextInt();
                }    
                changeboard(player2, row ,col);
                printMethod(boardMoves);
                if(checkWinner()){
                    System.out.println("The winner is player2.");
                        break;
                }
                if(checkTie()){
                    System.out.println("This is game is a tie.");
                        break;
                }
            }
    }
    public static void changeboard(char player, int row, int col)
    {
        boardMoves[row][col] = player; 
        
    }
    
     
    public static boolean checkMoves(int row, int column){
        if( (row>5 || column>5) || (row<1 || col<1) )       //Checks for out of bounds
            return true;
        
        else if( (row%2 == 0) || (col%2 == 0) )     //Checks if row and col enter is in the spots 1-9.
            return true;
        
        else if(boardMoves[row][column]=='X' || boardMoves[row][column] == 'O') //Checks if there was something there already.
            return true;

        return false;
    }
    public static boolean checkPlayer(String player){  
        if( (player.equals("X")) || (player.equals("O")) )      //If it does equal X or O then it would exit the while loop, if not it will stay true and stay in the while loop.
            return false;
            
        return true;
    }
    
    public static void printMethod(char[][] array){
        for(int row = 0; row < array.length; row++){
            for(int col = 0; col< array[0].length; col++){
                System.out.print(array[row][col] + " ");
            }
                System.out.println();
        }
    }
    public static boolean checkWinner() {
         if( boardMoves[1][1]==boardMoves[1][3] && boardMoves[1][3] == boardMoves[1][5] && (boardMoves[1][1]=='X' || boardMoves[1][1]=='O'))  //first row 
                return true;
    else if( boardMoves[3][1]==boardMoves[3][3] && boardMoves[3][3] == boardMoves[3][5] && (boardMoves[3][1]=='X' || boardMoves[3][1]=='O')) //second row
                return true;
    else if( boardMoves[5][1]==boardMoves[5][3] && boardMoves[5][3] == boardMoves[5][5] && (boardMoves[5][1]=='X' || boardMoves[5][1]=='O')) //thrid row
                return true;
    else if( boardMoves[1][1]==boardMoves[3][1] && boardMoves[3][1] == boardMoves[5][1] && (boardMoves[1][1]=='X' || boardMoves[1][1]=='O')) //first column 
                return true;
    else if( boardMoves[3][1]==boardMoves[3][3] && boardMoves[3][3] == boardMoves[3][5] && (boardMoves[3][1]=='X' || boardMoves[3][1]=='O')) //second column
                return true;
    else if( boardMoves[5][1]==boardMoves[5][3] && boardMoves[5][3] == boardMoves[5][5] && (boardMoves[5][1]=='X' || boardMoves[5][1]=='O')) //thrid column
                return true;
    else if( boardMoves[1][1]==boardMoves[3][3] && boardMoves[3][3] == boardMoves[5][5] && (boardMoves[1][1]=='X' || boardMoves[1][1]=='O')) //Diagonal top left to bottom right
                return true;
    else if( boardMoves[1][5]==boardMoves[3][3] && boardMoves[3][3] == boardMoves[5][1] && (boardMoves[1][5]=='X' || boardMoves[1][5]=='O')) //Diagonal bottom left to top right 
                return true;
    else
                return false;
    }


    public static boolean checkTie() 
    {
        for (int i = 0; i < boardMoves.length; i++){
            for (int p=0; p < boardMoves[i].length; p++){           //checks if anyone the spaces are 1-9, and if not that means all spaces are filled and therefore a tie
                if(boardMoves[i][p] == '1')         
                    return false;
                else if(boardMoves[i][p] == '2')
                    return false;
                else if(boardMoves[i][p] == '3')
                    return false; 
                else if(boardMoves[i][p] == '4')
                    return false;
                else if(boardMoves[i][p] == '5')
                    return false;
                else if(boardMoves[i][p] == '6')
                    return false;
                else if(boardMoves[i][p] == '7')
                    return false; 
                else if(boardMoves[i][p] == '8')
                    return false; 
                else if(boardMoves[i][p] == '9')
                    return false; 
            }
        }
            return true;
    }
}
