# tic-tac-toe-game
#include <iostream>
using namespace std;

// Display the game board
void displayBoard(char board[3][3])
{
    cout << "\n";
    cout << "     |     |     \n";
    cout << "  " << board[0][0] << "  |  " << board[0][1]
         << "  |  " << board[0][2] << "\n";
    cout << "_____|_____|_____\n";
    cout << "     |     |     \n";
    cout << "  " << board[1][0] << "  |  " << board[1][1]
         << "  |  " << board[1][2] << "\n";
    cout << "_____|_____|_____\n";
    cout << "     |     |     \n";
    cout << "  " << board[2][0] << "  |  " << board[2][1]
         << "  |  " << board[2][2] << "\n";
    cout << "     |     |     \n";
}

// Check whether a player has won
bool checkWin(char board[3][3], char player)
{
    // Check rows
    for (int i = 0; i < 3; i++)
    {
        if (board[i][0] == player &&
            board[i][1] == player &&
            board[i][2] == player)
        {
            return true;
        }
    }

    // Check columns
    for (int i = 0; i < 3; i++)
    {
        if (board[0][i] == player &&
            board[1][i] == player &&
            board[2][i] == player)
        {
            return true;
        }
    }

    // Check diagonals
    if (board[0][0] == player &&
        board[1][1] == player &&
        board[2][2] == player)
    {
        return true;
    }

    if (board[0][2] == player &&
        board[1][1] == player &&
        board[2][0] == player)
    {
        return true;
    }

    return false;
}

// Check whether the board is full
bool checkDraw(char board[3][3])
{
    for (int i = 0; i < 3; i++)
    {
        for (int j = 0; j < 3; j++)
        {
            if (board[i][j] == ' ')
            {
                return false;
            }
        }
    }

    return true;
}

int main()
{
    // Initialize 3x3 character matrix
    char board[3][3] =
    {
        {' ', ' ', ' '},
        {' ', ' ', ' '},
        {' ', ' ', ' '}
    };

    char currentPlayer = 'X';
    int row, col;

    cout << "=============================\n";
    cout << "       TIC-TAC-TOE GAME      \n";
    cout << "=============================\n";

    while (true)
    {
        displayBoard(board);

        cout << "\nPlayer " << currentPlayer << "'s turn.\n";
        cout << "Enter row (1-3): ";
        cin >> row;

        cout << "Enter column (1-3): ";
        cin >> col;

        // Validate row and column
        if (row < 1 || row > 3 || col < 1 || col > 3)
        {
            cout << "\nInvalid position! Enter values from 1 to 3.\n";
            continue;
        }

        // Convert to array index
        row--;
        col--;

        // Check whether position is already occupied
        if (board[row][col] != ' ')
        {
            cout << "\nPosition already occupied! Try again.\n";
            continue;
        }

        // Place player's symbol
        board[row][col] = currentPlayer;

        // Check for winner
        if (checkWin(board, currentPlayer))
        {
            displayBoard(board);
            cout << "\n*****************************\n";
            cout << "   Player " << currentPlayer << " WINS!\n";
            cout << "*****************************\n";
            break;
        }

        // Check for draw
        if (checkDraw(board))
        {
            displayBoard(board);
            cout << "\n*****************************\n";
            cout << "          GAME DRAW!\n";
            cout << "*****************************\n";
            break;
        }

        // Switch player
        if (currentPlayer == 'X')
            currentPlayer = 'O';
        else
            currentPlayer = 'X';
    }

    return 0;
}