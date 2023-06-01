# TicTacToe
# java
import java.util.Scanner;

public class TicTacToe {
    private static final int BOARD_SIZE = 3;
    private static final char PLAYER_X = 'X';
    private static final char PLAYER_O = 'O';
    private static final char EMPTY_CELL = ' ';

    private char[][] board;
    private char currentPlayer;

    public TicTacToe() {
        board = new char[BOARD_SIZE][BOARD_SIZE];
        currentPlayer = PLAYER_X;

        initializeBoard();
    }

    private void initializeBoard() {
        for (int i = 0; i < BOARD_SIZE; i++) {
            for (int j = 0; j < BOARD_SIZE; j++) {
                board[i][j] = EMPTY_CELL;
            }
        }
    }

    public void playGame() {
        boolean gameFinished = false;
        int totalMoves = 0;

        while (!gameFinished) {
            displayBoard();
            int row = getPlayerInput("Enter the row (1-" + BOARD_SIZE + "): ");
            int col = getPlayerInput("Enter the column (1-" + BOARD_SIZE + "): ");

            if (makeMove(row - 1, col - 1)) {
                totalMoves++;

                if (checkWin(row - 1, col - 1)) {
                    displayBoard();
                    System.out.println("Player " + currentPlayer + " wins!");
                    gameFinished = true;
                } else if (totalMoves == BOARD_SIZE * BOARD_SIZE) {
                    displayBoard();
                    System.out.println("It's a draw!");
                    gameFinished = true;
                } else {
                    currentPlayer = (currentPlayer == PLAYER_X) ? PLAYER_O : PLAYER_X;
                }
            } else {
                System.out.println("Invalid move. Please try again.");
            }
        }
    }

    private void displayBoard() {
        System.out.println("-------------");

        for (int i = 0; i < BOARD_SIZE; i++) {
            for (int j = 0; j < BOARD_SIZE; j++) {
                System.out.print("| " + board[i][j] + " ");
            }

            System.out.println("|");
            System.out.println("-------------");
        }
    }

    private int getPlayerInput(String message) {
        Scanner scanner = new Scanner(System.in);

        System.out.print(message);
        int input = scanner.nextInt();

        while (input < 1 || input > BOARD_SIZE) {
            System.out.print("Invalid input. " + message);
            input = scanner.nextInt();
        }

        return input;
    }

    private boolean makeMove(int row, int col) {
        if (board[row][col] == EMPTY_CELL) {
            board[row][col] = currentPlayer;
            return true;
        }

        return false;
    }

    private boolean checkWin(int row, int col) {
        if (board[row][0] == currentPlayer && board[row][1] == currentPlayer && board[row][2] == currentPlayer) {
            return true;
        }

        if (board[0][col] == currentPlayer && board[1][col] == currentPlayer && board[2][col] == currentPlayer) {
            return true;
        }
        if (board[0][0] == currentPlayer && board[1][1] == currentPlayer && board[2][2] == currentPlayer) {
            return true;
        }
        if (board[0][2] == currentPlayer && board[1][1] == currentPlayer && board[2][0] == currentPlayer) {
            return true;
        }

        return false;
    }

    public static void main(String[] args) {
        TicTacToe game = new TicTacToe();
        game.playGame();
    }
}
