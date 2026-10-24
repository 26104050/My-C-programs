# My-C-programs

#include <stdio.h>

char board[3][3] = {
    {'1', '2', '3'},
    {'4', '5', '6'},
    {'7', '8', '9'}
};

void display()
{
    int i;

    for (i = 0; i < 3; i++)
    {
        printf(" %c | %c | %c\n",
               board[i][0], board[i][1], board[i][2]);

        if (i < 2)
            printf("---|---|---\n");
    }
}

int checkWin()
{
    int i;

    for (i = 0; i < 3; i++)
    {
        if (board[i][0] == board[i][1] &&
            board[i][1] == board[i][2])
            return 1;

        if (board[0][i] == board[1][i] &&
            board[1][i] == board[2][i])
            return 1;
    }

    if (board[0][0] == board[1][1] &&
        board[1][1] == board[2][2])
        return 1;

    if (board[0][2] == board[1][1] &&
        board[1][1] == board[2][0])
        return 1;

    return 0;
}

int main()
{
    int choice, turn, row, col;
    char player;

    for (turn = 0; turn < 9; turn++)
    {
        display();

        player = (turn % 2 == 0) ? 'X' : 'O';

        printf("Player %c, enter position (1-9): ", player);
        scanf("%d", &choice);

        if (choice < 1 || choice > 9 ||
            board[(choice - 1) / 3][(choice - 1) % 3] == 'X' ||
            board[(choice - 1) / 3][(choice - 1) % 3] == 'O')
        {
            printf("Invalid position! Try again.\n");
            turn--;
            continue;
        }

        row = (choice - 1) / 3;
        col = (choice - 1) % 3;

        board[row][col] = player;

        if (checkWin())
        {
            display();
            printf("Player %c wins!\n", player);
            return 0;
        }
    }

    display();
    printf("Match Draw!\n");

    return 0;
}