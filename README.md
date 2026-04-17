#include <stdio.h>

char board[3][3];
char player = 'X';

void initBoard() {
    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++) board[i][j] = ' ';
}

void printBoard() {
    printf("\n  0   1   2\n");
    for (int i = 0; i < 3; i++) {
        printf("%d %c | %c | %c \n", i, board[i][0], board[i][1], board[i][2]);
        if (i < 2) printf("  --|---|--\n");
    }
}

int checkWin() {
    for (int i = 0; i < 3; i++) {
        // Check rows and columns
        if (board[i][0] == player && board[i][1] == player && board[i][2] == player) return 1;
        if (board[0][i] == player && board[1][i] == player && board[2][i] == player) return 1;
    }
    // Check diagonals
    if (board[0][0] == player && board[1][1] == player && board[2][2] == player) return 1;
    if (board[0][2] == player && board[1][1] == player && board[2][0] == player) return 1;
    return 0;
}

int main() {
    int row, col, turns = 0;
    initBoard();

    while (turns < 9) {
        printBoard();
        printf("\nPlayer %c, enter row and col (0-2): ", player);
        if (scanf("%d %d", &row, &col) != 2 || board[row][col] != ' ') {
            printf("Invalid move! Try again.\n");
            continue;
        }

        board[row][col] = player;
        if (checkWin()) {
            printBoard();
            printf("\nPlayer %c wins!\n", player);
            return 0;
        }

        player = (player == 'X') ? 'O' : 'X';
        turns++;
    }

    printBoard();
    printf("\nIt's a draw!\n");
    return 0;
}
