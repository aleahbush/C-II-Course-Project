# C-II-Course-Project
Skills
My name is Aleah Bush
I am a student learning IT in college to acheive my assosicates degree in Science. I've been studying IT for some time now and im almost at the end and hope to succed. Here I will be doing a TIC TAC TOE program as my final project. Im still in the process of trying to learn c++ fully and this will give me more expierence. To complete my Tic Tac Toe assignment i have steps to follow which is to make a 3X3 tic tac board in c++ method. Included in the board to function i have to use game rules, user input, exception handling,user interface, AI oppenent mode, and two player mode.


TIC TAC TOE 

#include <iostream>
#include <iomanip>
#include <cstdlib>
#include <ctime>

using namespace std;

#define SIZE 3x3

void playerVsPlayer();
void playerVsComputer();
void initializeBoard(char board[][SIZE]);
void displayBoard(char board[][SIZE]);
void playerTurn(char board[][SIZE]);
void playerXturn(char board[][SIZE]);
void playerOturn(char board[][SIZE]);
bool validMove(char board[][SIZE], int row, int col);
char gameStatus(char board[][SIZE]);
void computerTurn(char board[][SIZE]);

int main()
{
    int choice;
    while (1)
    {
        cout << "************MENU************" << endl;
        cout << "1.  Play against friend" << endl;
        cout << "2.  Play against the computer" << endl;
        cout << "3.  EXIT" << endl;
        // ask for user choice
        cout << "Enter your choice: ";   
        cin >> choice;  //input 
        if (choice == 1)
            playerVsPlayer();
        else if (choice == 2)
            playerVsComputer();
        else if (choice == 3)
        {
            cout << "\nBye Bye!!";
            return 0;
        }
        else
            cout << "Invalid Choice!" << endl;
    }
}

void playerVsPlayer()
{
    char board[SIZE][SIZE];
    int playerX = 0, playerO = 0;
    bool player;

    cout << "\nPlay against a friend." << endl;
    cout << "The first to win 3 games is the winner" << endl
         << endl;

    while (playerX < 3 && playerO < 3)
    {
        player = true;
        initializeBoard(board);

        while (gameStatus(board) == 'N')
        {
            displayBoard(board);
            if (player)
                playerXturn(board);
            else // player O turn
                playerOturn(board);
            player = !player;
        }

        displayBoard(board);

        if (gameStatus(board) == 'X')
        {
            cout << "Player X wins the round" << endl;
            playerX++;
        }
        else if (gameStatus(board) == 'O')
        {
            cout << "Player O wins the round" << endl;
            playerO++;
        }
    }

    if (playerX == 3)
        cout << endl
             << "Player X is the winner of 3 games!!!" << endl
             << endl;
    else
        cout << endl
             << "Player O is the winner of 3 games!!!" << endl
             << endl;
}

void playerVsComputer()
{
    cout << "\nPlay against the computer." << endl;
    srand(time(NULL));
    char board[SIZE][SIZE];
    int playerWins = 0, computerWins = 0;
    bool player;

    cout << "The first to win 3 games is the winner" << endl
         << endl;

    while (playerWins < 3 && computerWins < 3)
    {
        player = true;
        initializeBoard(board);

        while (gameStatus(board) == 'N')
        {
            displayBoard(board);
            if (player)
                playerTurn(board);
            else // computer turn
                computerTurn(board);
            player = !player;
        }

        displayBoard(board);

        if (gameStatus(board) == 'X')
        {
            cout << "Player wins the round" << endl;
            playerWins++;
        }
        else if (gameStatus(board) == 'O')
        {
            cout << "Computer wins the round" << endl;
            computerWins++;
        }
    }

    if (playerWins == 3)
        cout << endl
             << "Player is the winner of 3 games!!!" << endl
             << endl;
    else
        cout << endl
             << "Computer is the winner of 3 games!!!" << endl
             << endl;
}

void initializeBoard(char board[][SIZE])
{
    for (int i = 0; i < SIZE; i++)
    {
        for (int j = 0; j < SIZE; j++)
            board[i][j] = '?';
    }
}

void displayBoard(char board[][SIZE])
{
    cout << endl
         << setw(3) << "";
    for (int i = 1; i <= SIZE; i++)
    {
        cout << setw(3) << i;
    }

    for (int i = 0; i < SIZE; i++)
    {
        cout << endl
             << setw(3) << (i + 1);
        for (int j = 0; j < SIZE; j++)
        {
            cout << setw(3) << board[i][j];
        }
        cout << endl;
    }
}

void playerTurn(char board[][SIZE])
{
    int row, col;
    cout << "Choose where to insert your 'X' mark, insert row then column: ";
    cin >> row >> col;
    while (!validMove(board, row - 1, col - 1))
    {
        cout << "Invalid row or/and column" << endl;
        cout << "Choose where to insert your 'X' mark, insert row then column: ";
        cin >> row >> col;
    }

    board[row - 1][col - 1] = 'X';
}

void computerTurn(char board[][SIZE])
{
    int row, col;
    row = rand() % 3;
    col = rand() % 3;

    while (!validMove(board, row, col))
    {
        row = rand() % 3;
        col = rand() % 3;
    }

    board[row][col] = 'O';
    cout << "Computer chose " << (row + 1) << " " << (col + 1) << endl;
}

void playerXturn(char board[][SIZE])
{
    int row, col;
    cout << "Player X turn:" << endl;
    cout << "Choose where to insert your 'X' mark, insert row then column: ";
    cin >> row >> col;
    while (!validMove(board, row - 1, col - 1))
    {
        cout << "Invalid row or/and column" << endl;
        cout << "Choose where to insert your 'X' mark, insert row then column: ";
        cin >> row >> col;
    }
    
    board[row - 1][col - 1] = 'X';
}

void playerOturn(char board[][SIZE])
{
    int row, col;
    cout << "Player O turn:" << endl;
    cout << "Choose where to insert your 'O' mark, insert row then column: ";
    cin >> row >> col;
    while (!validMove(board, row - 1, col - 1))
    {
        cout << "Invalid row or/and column" << endl;
        cout << "Choose where to insert your 'O' mark, insert row then column: ";
        cin >> row >> col;
    }

    board[row - 1][col - 1] = 'O';
}

bool validMove(char board[][SIZE], int row, int col)
{
    return (row >= 0 && row < SIZE && col >= 0 && col < SIZE && board[row][col] == '?');
}

// Function to return the game status
// X - player wins
// O - computer wins
// T - Tie
// N - In progress, No result
char gameStatus(char board[][SIZE])
{
    char status = 'T'; // initialize status to tie

    for (int i = 0; i < SIZE; i++)
    {
        if (board[i][0] == board[i][1] && board[i][0] == board[i][2])
        {
            if (board[i][0] == 'X')
                status = 'X';
            else if (board[i][0] == 'O')
                status = 'O';
        }

        
        if (board[0][i] == board[1][i] && board[0][i] == board[2][i])
        {
            if (board[0][i] == 'X')
                status = 'X';
            else if (board[0][i] == 'O')
                status = 'O';
        }
    }

    if (board[0][0] == board[1][1] && board[0][0] == board[2][2])
    {
        if (board[0][0] == 'X')
            status = 'X';
        else if (board[0][0] == 'O')
            status = 'O';
    }

   
    if (board[0][2] == board[1][1] && board[1][1] == board[2][0])
    {
        if (board[1][1] == 'X')
            status = 'X';
        else if (board[1][1] == 'O')
            status = 'O';
    }

    if (status == 'T')
    {
    
        for (int i = 0; i < 3; i++)
        {
            for (int j = 0; j < 3; j++)
            {
                if (board[i][j] == '?') // empty slot, change status to No result
                    status = 'N';
            }
        }
    }
    return 0;
}
